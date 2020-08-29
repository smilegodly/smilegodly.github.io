---
layout: post
title: "Contributing to Open Source Projects"
date: 2019-09-22
---
I have filed 2 issues and submitted 2 separate pull requests for each issue this week on other students open source web applications.

The first issue I filed was #10 on Grommers00’s application. [https://github.com/Grommers00/my-note/issues/10](https://github.com/Grommers00/my-note/issues/10)
After talking about the issue with Grommers00 about the problem of having a restore point as well as auto-saves, I thought of a solution which included a visual countdown timer on the page so that the user can see when the restore point would be getting overwritten. 
I implemented that solution as #11 , and it was merged by Grommers00 on the master branch shortly after. [https://github.com/Grommers00/my-note/pull/11](https://github.com/Grommers00/my-note/pull/11)
The code for the timer on the web page is as follows:


{% highlight js %}
function startTimer(duration, display) {
    var timer = duration, seconds;
    setInterval(function () {
        seconds = parseInt(timer % 60, 10);
        display.textContent =seconds;
        if (--timer < 0) {
            timer = duration;
        }
    }, 1000);
}
window.onload = function () {
    var twentysec = 20,
        display = document.querySelector('#time');
    startTimer(twentysec, display);
};
{% endhighlight %}



The second issue I filed was #8 on jrdnlx’s application. [https://github.com/jrdnlx/noteboard/issues/8](https://github.com/jrdnlx/noteboard/issues/8)
I noticed that the application was not saving any data that the user was inputting. 
I fixed the save issue in the pull request #9. [https://github.com/jrdnlx/noteboard/pull/9](https://github.com/jrdnlx/noteboard/pull/9)
The code for the bug fix is as follows:

{% highlight js %}
document.addEventListener("DOMContentLoaded", () => {
    fs.readFile('/note', 'utf-8', function(err, data){
        if(data != null){
            //display data in the file
            document.getElementById("note").innerHTML=data
        }
        else if(err != null){
            //display "Welcome to my notepad!"
            document.getElementById("note").innerHTML="Welcome to my Notepad!"
        }
    });
});

var save = function(){
    fs.writeFile('/note',document.querySelector('#note').innerHTML, function(err){
        if(err!=null){
            console.log(err);
        }
    });
}

setInterval(save, 3000);
{% endhighlight %}
