FROM ksoichiro/android

MAINTAINER ksoichiro "soichiro.kashima@gmail.com"

RUN echo y | android update sdk --filter platform-tools,build-tools-23.0.3,sysimg-23,android-23,extra-android-support --no-ui --force

# Set up and run emulator
RUN echo no | android create avd --force -n test -t android-23
# Avoid emulator assumes HOME as '/'.
ENV HOME /root
ADD wait-for-emulator /usr/local/bin/
ADD start-emulator /usr/local/bin/

RUN mkdir -p /opt/tmp && android create project -g -v 0.9.+ -a MainActivity -k com.example.example -t android-23 -p /opt/tmp
RUN cd /opt/tmp && ./gradlew tasks
RUN rm -rf /opt/tmp

VOLUME /workspace
WORKDIR /workspace
