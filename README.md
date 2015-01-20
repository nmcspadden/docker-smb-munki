# docker-smb-munki
SMB share for /munki_repo

Simple SMB share designed specifically for the [Munki Docker container](https://github.com/nmcspadden/docker-munki).

To Use:
----
Assuming you have a data-only container called munki-data:  
`docker run -d -p 445:445 --volumes-from munki-data --name smb nmcspadden/smb-munki /munki_repo`

You may have to change permissions on /munki_repo to allow for read-write privileges by a guest:  
`docker exec smb chown -R nobody:nogroup /munki_repo/`  
`docker exec smb chmod -R ugo+rwx /munki_repo/`

From an OS X client:  
Finder -> Go -> Connect to Server -> smb://docker-host-ip/  
Connect as a guest.  

You should have read-write privileges on the share.  Use the appropriate Munki tools (munkiimport, manifestutil, makecatalogs, etc.) to populate the Munki repo.
