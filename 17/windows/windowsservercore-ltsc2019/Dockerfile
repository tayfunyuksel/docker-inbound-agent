# escape=`
# The MIT License
#
#  Copyright (c) 2019, Alex Earl
#
#  Permission is hereby granted, free of charge, to any person obtaining a copy
#  of this software and associated documentation files (the "Software"), to deal
#  in the Software without restriction, including without limitation the rights
#  to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
#  copies of the Software, and to permit persons to whom the Software is
#  furnished to do so, subject to the following conditions:
#
#  The above copyright notice and this permission notice shall be included in
#  all copies or substantial portions of the Software.
#
#  THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
#  IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
#  FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
#  AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
#  LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
#  OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
#  THE SOFTWARE.

ARG version=3107.v665000b_51092-5
FROM jenkins/agent:${version}-jdk17-windowsservercore-ltsc2019

LABEL Description="This is a base image, which allows connecting Jenkins agents via JNLP protocols on Windows" Vendor="Jenkins Project" Version="$version"

ARG user=jenkins

RUN $output = net users ; `
    if(-not ($output -match $env:user)) { `
        net accounts /maxpwage:unlimited ; `
        net user "$env:user" /add /expire:never /passwordreq:no ; `
        net localgroup Administrators /add $env:user ; `
        Set-LocalUser -Name $env:user -PasswordNeverExpires 1 `
    }

COPY jenkins-agent.ps1 C:/ProgramData/Jenkins
USER ${user}
ENTRYPOINT ["powershell.exe", "-f", "C:/ProgramData/Jenkins/jenkins-agent.ps1"]
