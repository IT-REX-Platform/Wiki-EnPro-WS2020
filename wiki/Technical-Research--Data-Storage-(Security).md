# Potential attacks

- attacks on infrastructure
	- overwrite existing file (including critical files such as .htaccess to launch attacks on the server)
	- storing the file in a bad location
	- malicious file that leverages vulnerability in server-side file handling
		- gain control of server (e.g. upload .php, call it and the server executes it)
- attacks on users
	- malicious content that may infect users' machines
	- xss / phishing
- dos
	- large files
	- special cases that the server can't handle (filename characters / length / etc.)
		- bug in serverside software (zip-bomb, etc.)
- legal trouble
	- upload malware command & control data
	- upload (illegal) adult content
	- upload illegal software
	- violence and harassment messages

=> depends on what the application does with the uploaded file and especially where it stores it


# Problem sources

- file metadata
	- path
	- file name
- file size or content

---

# How to prevent vulnerabilities / combat potential attacks

### Implementation-specific

- only allow specific file types
	- whitelist
	- check filename extension
	- verify file type (e.g. check magic bytes)
- authenticate users and keep records
	- -> logging mechanism needs to be protected as well!
		- -> log forgery
		- -> code injection
- naming restrictions (prior to renaming for storage)
	- maximum length
	- restrict characters
		- whitelist
		- sample regex:  
			[a-zA-Z0-9]{1,200}\.[a-zA-Z0-9]{1,10}
	- discard special characters
		- discard additional .*%$
	- randomize uploaded file names
		- random identifier
		- probably not a good idea to use a hash or anything the user can guess/predict
		- => real location of file can't be guessed by user
		- still, prevent overwrites *just* in case
- maximum file size
	- minimum file size to combat dos
- store files outside of web root folder (website's public directory)
	- => can't be executed via assigned path URL
- use simple error messages
	- i.e. when file upload fails for some reason, don't include revealing information in your error message
		- such as paths, file names, server config, etc.

- use csrf protection methods (see system & web security slides)
	- tokens
	- use frameworks if applicable
- cors
	- only enable for static or publicly accessible data
	- otherwise, "Access-Control-Allow-Origin" header should only contain authorised addresses
	- remove items within headers that are not required
- try to use POST instead of PUT or GET

- add "Content-Disposition: Attachment" and "X-Content-Type-Options: nosniff" to secure website against flash or pdf-based cross-site content-hijacking attacks
	- recommended to add this for all files that user needs to download / all modules that deal with file download
- remove flash/pdf (crossdomain.xml) or silverlight (clientaccesspolicy.xml) cross-domain policy files
	- disable browser caching for these files

- scan for malware
- remove embedded objects/threats (content disarm and reconstruction / cdr)
	- e.g. strip macros from office files
- if we allow upload of compressed files, check each file individually after decompression
- check files for known vulnerabilities

### Setup

- check file upload module's access controls
- check file upload directories' permissions (no execute, exclude all script handlers)
- keep server software up-to-date, especially tools and libraries that deal with user uploads
- consider saving files in a database rather than on the filesystem
- consider using isolated server with different domain to serve uploaded files
- remove write permission from files and folders other than the upload folder
- configure server to ignore critical config files (.htaccess, web.config) in upload directories in case a user manages to drop one
- ensure that files with double extensions (e.g. file.php.txt) can't be executed
- ensure that uploaded files can't be accessed by unauthorized users


### Good practices

- validate metadata extremely carefully
- analyse everything our application does with files
- think carefully about what processing and interpreters are involved

---

\
Sample attacks can be found at https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload

# Sources

https://www.opswat.com/blog/file-upload-protection-best-practices
https://owasp.org/www-community/vulnerabilities/Unrestricted_File_Upload

