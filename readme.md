## Goal
To have the "latest" file (json, yaml or anything else) which contains the latest version data.  
And ordered list of .patch files which allows to get a previous versions of data.

### How to do update
```
cp   latest.data old.data
vim  latest.data                                         # update data
diff latest.data old.data > back_to_version_NNN.patch    # naming should keeps order in patches list
rm   old.data
```
- As result here we should have:
  - updated data in "latest" file
  - a new patch file.


### Check a list of patches to previous versions
```
ls -r1 *.patch
```

### How to get previous version
```
cp latest.data old.data

#                                 + - get a data file of N (in this case 2) versions far from latest
#                                 |
#                                -+-
for el in $(ls -r1 *.patch | head -2); do echo -n "$el -> ";  patch old.data $el; done

cat old.data                      # check priveus version or do something else with it
rm  old.data                      # remove it
```
