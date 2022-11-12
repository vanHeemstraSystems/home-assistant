# 200 - Manage Docker as a non-Root user

I find it easiest if I can manage Docker as a non-Root user – it means I don’t need to add *sudo* to the start of every command. This may reduce the security of my Docker environment, but because it’s running in my own network, inaccessible from the outside world I’m willing to accept that risk.

To get Docker to work as a non-root user we need to add our user to the Docker group. Let’s do that now. See also https://stackoverflow.com/questions/70369278/how-to-add-the-current-user-to-the-docker-group-on-macos

List the existing user groups with ```dscl . list /groups```

To create a user group (here: docker), if it doesn't exist use the command ```sudo dscl . create /Groups/<groupName>```.

```
sudo dscl . create /Groups/docker
```

Now add your user account to that Docker group.

```
sudo dseditgroup -o edit -a $USER -t user docker
```

To test and see if the expected user has been added to the specific group (here: docker) one can use the command ```dscl . -read /Groups/docker GroupMembership``` to list all the members. However, it is not guaranteed to deliver the correct result, as explained [here](https://superuser.com/a/395738/588662).

Now log out and back in again for the permission changes to take effect. If everything has worked properly, you should be able to re-download and run the Hello World Docker container without using sudo.

```
docker run hello-world
```
