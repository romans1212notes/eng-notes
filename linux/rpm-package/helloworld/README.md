# helloworld example
In this directory, run this:
```
copy hello-world.sh ~/
cp -r rpmbulid ~/
```

In $HOME directory, run this:
```
# sudo yum install rpm-build
rpmbuild -bb rpmbuild/SPECS/hellowworld.spec
```

Another way is to create a link to rpmbuild in home directory.

# docs
* http://tmurray3.blogspot.com/2010/11/building-rpm-packages-for-java-from-jar.html
* https://fedoraproject.org/wiki/How_to_create_an_RPM_package
