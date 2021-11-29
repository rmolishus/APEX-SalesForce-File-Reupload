Motivation:
This code was created to solve a problem where files in Salesforce had too many versions associated with them. 
This can be viewed in a file's detail page. 
Salesforce doesn't let you delete these unecessary versions, which take up the sum of those versions' content size in file storage.
The only way to get rid of those versions is to delete the file and upload a copy of whatever version(s) you want.
However, one limitaion of this is if your files are shared with users/objects.
I needed my files to be shared with the same users/objects as before.
I couldn't find something that already did this in bulk, so I hope this can help soomeone with the same problem out.
This isn't the most efficient or elegant code, but it does the job. If you have possible improvements, feel free to share them.

How it works (Overview):
This code gets all files with more than 1 version.
For each file, it copies the latest version of the file and 1 of it's links to an object/user/etc.
Once these have been inserted, it deletes the old file. 

Possible Modifications:
-Currently, the original Salesforce created date is appended to the new file's title.
	To get rid of this or modify it's placement, change the title assignment and/or remove the code the gets the created date.
-Currently, the code only retrieves 1 CDL(ContentDocumentLink) per file. This was done to get around triggers and other obstacles in my org.
	You can change this by adding a loop to the CDL creation portion of the code. 
	Note: Doing this WILL impact/lower how many files can be processes at once.
-To add a CDL to a user:
	1.ShareType should be set to 'V' for viewer, otherwise you may get an error
	2. If the file was previously owned by another user, they will now be set as a viewer.
	   -The account who runs the code will be set as the new owner.
	3. To 'reupload' a document owned by the user running the code, exclude the user's Id from the CDL query or add a try to the CDL insert.
		-Uploading the new ContentVersion automatically adds a CDL to the owner (user running the script).
		-Trying to add a 'duplicate' linkedEntity will result in an error

Final Thoughts:
I couldn't find something that already did this in bulk, so I hope this can help soomeone with the same problem out.
This isn't the most efficient or elegant code, but it does the job. If you have possible improvements, feel free to share them.
Code by: Rebecca Molishus
Last updated: Novemember 2021