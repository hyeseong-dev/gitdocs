# PPA로 파이썬 설치

You are getting that error because you first need to update the package list and the prerequisites.

```text
sudo apt update
sudo apt install software-properties-common
```

Then, add the repo ppa:deadsnakes/ppa to your sources list \(where you will download python from\)

```text
sudo add-apt-repository ppa:deadsnakes/ppa
```

Make sure to press enter when prompted.

Lastly, install the version of your choice

```text
sudo apt install python3.9
```

Make sure to read this:

> Disclaimer: there's no guarantee of timely updates in case of security problems or other issues. If you want to use them in a security-or-otherwise-critical environment \(say, on a production server\), you do so at your own risk.

