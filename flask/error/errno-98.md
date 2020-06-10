# Errno 98

![](https://miro.medium.com/max/250/1*wpYx7nRVNmJLBFSG3dcg4g.jpeg)

I am working on a small flask project.

I have been working within a virtual environment with python 2.7. So I migrated to version 3.7.

Every time I start the server, I run into this error,

_OSError: \[Errno 98\] Address already in use_

Here is the solution.

Enter the following commands in the terminal

_**\|** ps -fA \| grep python_

This will select and display all the processes with python matching pattern

Check the one with “flask” in the path and note down its PID\(process ID\). This should be the second column of the output.

Then enter this command

**\|** kill -9 pid

Replace pid with the PID from the previous command

Then Restart your server

\| flask run

And it works!!

### About Me <a id="908b"></a>

I am Teresia Wangari, Currently studying Computer Science at the Catholic University of Eastern Africa, Nairobi, Kenya. I am the Developer Students Clubs, lead for the Catholic University of Eastern Africa, Nairobi, Kenya.



출처:   
[https://medium.com/@tessywangari05/oserror-errno-98-address-already-in-use-flask-error-ccbff65e2bb5](https://medium.com/@tessywangari05/oserror-errno-98-address-already-in-use-flask-error-ccbff65e2bb5)

