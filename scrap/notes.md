socket.io


Gotta check the active fetch (like signalR) on js, e.g live messaging app:
https://www.youtube.com/watch?v=CK2XEyVGc6c

https://github.com/MoienTajik/AspNetCore-Developer-Roadmap


https://ab--g4.netlify.app/vs/gumroad/

ghost.org


Jordan Peterson

https://undesign.learn.uno/ //uhh so... allround 

- BOM:
http://en.wikipedia.org/wiki/Byte_order_mark
http://stackoverflow.com/questions/2558172/utf-8-bom-signature-in-php-files

CSS BEM

https://30secondsofinterviews.org/

https://dmitripavlutin.com/simple-but-tricky-javascript-interview-questions/

https://www.toptal.com/javascript/interview-questions

https://flukeout.github.io/ //CSS selector practice

https://github.com/danrl/wifi-probe

https://github.com/brannondorsey/sniff-probes


https://ghygen.hi-folks.dev/?template=laravelapp

https://www.dvc.edu/future/steps/new.html


https://github.com/danielmiessler/SecLists

https://www.tindie.com/products/stephanelec/mooltipass-mini-ble-authenticator/

https://prometheus.io/

Prometheus video https://www.youtube.com/watch?v=4WWW2ZLEg74


/* 
I know it is already too late, but maybe some of you still have an unaffected MyBook.

I would like to share with you how to fix the security vulnerability CVE-2018-18472:

Access SSH and edit file (e.g. with “nano”)
/var/www/Admin/webapp/includes/languageConfiguration.php

First change
Search for:

exec("sudo bash -c '(echo \"language {$changes["language"]}\">/etc/language.conf)'", $output, $retVal);
Replace with:

if (!preg_match('/^[a-z]{2}_[A-Z]{2}$/', $changes["language"], $dummy)) return 'BAD_REQUEST';
exec("sudo bash -c '(echo '\"'\"".escapeshellarg("language {$changes["language"]}")."\"'\"'>/etc/language.conf)'", $output, $retVal);
Second change:
Search for:

exec("sudo bash -c '(echo \"language {$lang["language"]}\">/etc/language.conf)'", $output, $retVal);
Replace with:

if (!preg_match('/^[a-z]{2}_[A-Z]{2}$/', $lang["language"], $dummy)) return 'BAD_REQUEST';
exec("sudo bash -c '(echo '\"'\"".escapeshellarg("language {$lang["language"]}")."\"'\"'>/etc/language.conf)'", $output, $retVal);
See, this is all you need to do. WD knew about this bug in 2018 and they refused to change these TWO LINES of code, just because the product is “EndOfLife”…

Of course, there might be other bugs, but this is the biggest of all. I am not aware of other code injection bugs, but I will now review the code and see if there is more. I really would like to keep my MyBook because I hate throwing working hardware away…

EDIT: My first version contained an error. This is the correct one!!!
Note: The preg_match line is not required to fix the vulnerability, but it avoids that hackers write garbage in your /etc/language.conf file.

EDIT 2: My code review is done. I did not find further root command injections which don’t require authentication

EDIT 3: Additional security settings you should consider

Disable “remote access” in the UI
Change “connection options” from “automatic” to “manual”, this disables UPnP
(thanks to @WDMyBookDead for that hint! They posted a screenshot)
Disable UPnP in your router
Disable factory reset:
If you believe that you will never need the factory restore, I recommend disabling it completely.
Edit /usr/local/sbin/factoryRestore.sh and wipeFactoryRestore.sh and change line #2 to exit.
*/ from https://community.wd.com/t/help-all-data-in-mybook-live-gone-and-owner-password-unknown/268111/415


Maze Generation Algorithm (https://en.wikipedia.org/wiki/Maze_generation_algorithm)


https://themodularbody.com/




https://www.youtube.com/channel/UC6IivHdACKC_wDc1kPWidNg
https://www.youtube.com/watch?v=hVLjCrxKfQM (important)
https://www.youtube.com/watch?v=JvbIEimqd0Y
https://back7.co/home/raspberry-pi-recovery-kit
https://archive.org/details/military-manuals
https://evanmeaney.com/_recpi.html

https://evanmeaney.com/currently.html (mindjob)
