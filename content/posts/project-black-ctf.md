+++
authors = ["Naman Arora"]
title = "Project Black CTF Walkthrough (Challenge 5)"
date = "2025-09-23"
description = "Project Black CTF Walkthrough for Challenge 5"
tags = [
 "Pentesting",
]
categories = [
 "Pentesting",
]
series = ["Pentesting"]
+++


# Intro


Recently, I saw a job posting for a [Graduate Penetration Tester](https://www.linkedin.com/posts/eddiez-me_graduate-penetration-tester-job-in-melbourne-activity-7371319398260916225-JREE) from the company Project Black. Although I didn't make the cut to qualify for the role (600+ people applied - talk about brutal lol), I was able to find all 6 flags for their CTF. In this blog post, I will go through challenge 5 from their website.

The challenge starts with a link to challenge5.txt which is an empty looking file on their website at [https://projectblack.io/ctf/challenge5.txt](https://projectblack.io/ctf/challenge5.txt). We can download the file for further analysis.

{{< figure src=/images/project-black-ctf/image1.png >}}

Uploading the file to cyberchef reveals that there are 2 characters in the file. This hinted at the file containing some sort of binary information.

{{< figure src=/images/project-black-ctf/image2.png >}}

I wrote this python script in order to read all bytes and replace them with either 1 or 0. This creates a binary representation of the contents that we can further analyse. I wasted some time on this step as I was not sure which byte they expected to be `1` and which byte to be `0`.

```python
filename = "/home/kali/project-black/challenge5.txt"
binary = ""

with open(filename, 'rb') as f:
   while True:
       byte = f.read(1)
       if not byte:  # If read() returns an empty, it's the end of the file
           break
       #print(f"Read byte: {byte} (integer value: {int.from_bytes(byte, 'big')})")
       if int.from_bytes(byte, 'big') == 32:
           binary += "0"
       else:
           binary += "1"

print(binary)
```

Analysis in cyberchef reveals another web url!

{{< figure src=/images/project-black-ctf/image3.png >}}

Accessing the website we see a login page asking us for a username and password.

{{< figure src=/images/project-black-ctf/image4.png >}}

Analysing the source of the webpage results in another cipher!

{{< figure src=/images/project-black-ctf/image5.png >}}

We go to cyberchef again to get our first flag!

{{< figure src=/images/project-black-ctf/image6.png >}}

```bash
Flag 1: PRJBLK{1/6:_fIR$t_0f_m@nY_fL@gz._wHEr3_W1lL_Y0u_pUT_Th3M_@1l?}
```

Upon accessing the `api/listing.php` file that is mentioned in the decoded cipher, we are greeted with another flag and the list of files on the webserver.

{{< figure src=/images/project-black-ctf/image7.png >}}

```bash
Flag 2: PRJBLK{2/6:_oH_b0y,_Wh@t_d0_W3_H@vE_hEr3}
```

Now flag 3 is kind of interesting because I found flag 4 before it. However, to keep things in order, here is how to discover flag 3.

{{< figure src=/images/project-black-ctf/image8.png >}}

If we go through the files listed, we will see a `.git` folder which is exposed in the `/app/dist/` directory. This means that we can access the `git` objects of the website.

{{< figure src=/images/project-black-ctf/image9.png >}}

We can now use the tool `git-dumper` to clone the repository being exposed on the website.

{{< figure src=/images/project-black-ctf/image10.png >}}

Upon further analysis of the project, `api/login.php` is discovered which contains the logic used by the website for authentication along with the 3rd flag!

{{< figure src=/images/project-black-ctf/image11.png >}}

```bash
Flag 3: PRJBLK{3/6:_H@v3_y0U_Con$1dEr3d_g1tt1nG_g00D???}
```

Now, going back to `/api/listing.php`, we discover some other `php` files. One of the interesting files also being exposed in the `/api` directory is the `users.php` file.

{{< figure src=/images/project-black-ctf/image12.png >}}

The last entry in the file contains the next flag!

{{< figure src=/images/project-black-ctf/image13.png >}}

```bash
Flag 4: PRJBLK{4/6:_An0th3r_d@y,_@n0th3r_fl@g._g0Tt@_c@tch_Em_@l1}
```

Now, if we go back to the `login.php` file that we saw in the project files, we will notice a comment which mentions `type juggling`.

```php
* TODO my boss said juggling is bad, don't know what that's
*      supposed to be mean bedtime reading:
*
*   https://www.php.net/manual/en/language.operators.comparison.php
```

`Type Juggling` is basically caused when developers use loose comparison for comparing values when strict comparison should have been used. For different types such as a `sha256` value, the value is converted to a mathematical representation. When comparing this value with a different type `PHP` will convert both variables to a common representation. In such cases, we may see an unexpected boolean value appear as a result of a comparison. There are similar issues in `Javascript` as well. There is a much better explanation of this here: [https://secops.group/php-type-juggling-simplified/](https://secops.group/php-type-juggling-simplified/)

The vulnerable line is as follows:

```php
if (hash('sha256', $password) != $targetUser['password']) {
```

Here, the usage of the loose comparator `!=` is a problem. We can try to find users with a similar password hash to a sha256 hash collision. We can find such collisions from [https://github.com/spaze/hashes/blob/master/sha256.md](https://github.com/spaze/hashes/blob/master/sha256.md).

{{< figure src=/images/project-black-ctf/image14.png >}}

From the `users.php` file, we saw that the user `eddie` has a password hash starting from `e0`.

{{< figure src=/images/project-black-ctf/image15.png >}}

Using the following creds logs us in the website. User: `eddie` and Password: `34250003024812`. Other passwords starting from `e0` will also work because of the same vulnerability as explained above.

This gives us the 5th flag!

```bash
Flag 5: PRJBLK{5/6:_D0_pHp_D3v310pEr$_Ev3r_LE@rN?}
```

Upon clicking the button titled `Click Me!`, the website sends a `POST` request to `flag.php`. If we analyse the `flag.php` file from the project files that we got using `git-dumper`, we'll see the following code.

```php
$role = $token['role'];
if ($role !== 'admin') {
   http_response_code(401); // Unauthorized
   $response['message'] = "Sorry, you don't have permission to see the flag :(";
   echo json_encode($response);
   exit();
}

$response = [
   'success' => true,
   'message' => file_get_contents('/app/config-files/flag6.txt'),
];
echo json_encode($response);
```

It seems that we're sending a token which contains a `role` variable which determines the content of the response. Upon looking closer at the request, we can see a `JWT` token being sent in the request.

{{< figure src=/images/project-black-ctf/image16.png >}}

Decoding the token on `jwt.io`, we can see more details encoded in the token. It seems that the token signature is not being verified.

{{< figure src=/images/project-black-ctf/image17.png >}}

We will use the encoder on the same website to modify the `role` from `user` to `admin`. This will get us an updated token that we can use to modify and resend the request from Firefox.

{{< figure src=/images/project-black-ctf/image18.png >}}

We can now modify and resend the request as shown below.

{{< figure src=/images/project-black-ctf/image19.png >}}

This time the request goes through and we can collect our final flag!

{{< figure src=/images/project-black-ctf/image20.png >}}

```bash
Flag 6: PRJBLK{6/6:_N0_$1gN1nG,_N0_W0rR13$}
```

# Final Thoughts


This was a really fun CTF and I wish more cyber jobs start using similar methods for testing candidates. I feel like more people applied to this position _because_ Project Black decided to challenge the participants like this. People love a good challenge ;)