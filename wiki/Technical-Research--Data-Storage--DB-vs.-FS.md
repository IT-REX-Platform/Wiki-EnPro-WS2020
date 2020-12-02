# Storing files in the database: pros and cons

## Pros
	- acid consistency / files and db in snyc; rollback of update is complicated when files are stored outside of db
	- backups automatically include files
	- security implications
	- more scalable in multi-server scenario
		- failover and availability concerns

## Cons
	- security implications (write handler to stream content from db; more attack surface)
	- people might rearrange files, breaking the link between them and the db entry
	- binary file object size limit
	- increases size of database
	- decreased portability (sql server's FILESTREAM object)
	- possible additional layer wrapped around the file (Ole object for example)
	- can't really use cloud storage

## General recommendation for IT-Rex:
	- store in filesystem, not in database;
	- maybe store paths in database
	- maybe use custom routes
		- map to file
		- store route in db

## Reasoning:
	- we're going to have files with sizes of different magnitudes (few MB for slides, hundreds of MBs for lecture recodings)
	- recordings probably too large even for modern DBMS
	- mixed approach probably not a good idea
		- if we have to implement proper handling for recordings, there's no reason not to incorporate smaller files as well


## Sources:

https://softwareengineering.stackexchange.com/questions/150669/is-it-a-bad-practice-to-store-large-files-10-mb-in-a-database  
https://dba.stackexchange.com/questions/2445/should-binary-files-be-stored-in-the-database  
https://dba.stackexchange.com/questions/736/is-it-better-to-store-images-in-a-blob-or-just-the-url  

**Extra**: semi-relevant paper (a bit dated though):  
https://www.microsoft.com/en-us/research/wp-content/uploads/2006/04/tr-2006-45.pdf
