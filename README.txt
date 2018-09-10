--------------------------------------------------------------------------------
	ESRLabs_DOORS_Export.dxl
	
	DXL Script to perform an export of requirements based on a set of filters
	define by the task defined on the "Homework_ESRLabs.pdf", contained on this
	repository.
	
	It shall fulfill all the mentioned requirements, although, there was no
	possibility to test the script due to lack of access to a DOORS client.
	
	Time to creation: ~8 h
	Time complexity: not evaluated
	Space complexity: not evaluated
	
	Developed by:
		Luis Teixeira @ 10/09/2018 
		luisteixeira@vodafone.pt
	
	Script Repository: 
		
	
--------------------------------------------------------------------------------

	IBM DOORS requirements:
	
	Due to some of the features implemented, version 9.3 or above is required 
	for the script to operate correctly.
	
	Example:
		for Link in each(Object obj) <- (string linkModuleName) do { }
		--> as stated on the DXL reference manual, requires Rational DOORS 9.3
		
--------------------------------------------------------------------------------

Three likely sources of error could be identified but not tested due to the
lack of access to a DOORS client. These are highlighted below:

[1]: 	The error exception functions might generate unintended errors.
		Without being able to test with the client and with a folder structure,
		it is not clear what exactly is the expected behavior when handling
		the folders and modules.
		
		A function should be created to test that:
			- The Folder "Interview" exists, contains the module "ESR_Interview"
			- The Folder and the module can be opened by the user
			- same procedure for the "ESR_Interview" and "ESR_Interview_Links"

[2]:	Could not find in the DXL Reference manual if the LinkFolder name can
		be obtained similarly to the LinkModule name. For that reason, lines 
		116 and 118 have been commented out. This would need to be tested and
		included if functional, as it would be necessary to check both that the
		link objects are matching both the expected Folder and Module names for
		the links.

[3]:	It is also not clear what is the most appropriate function to display
		notifications and error messages, hence the usage of both the "ack" and 
		the "print" functions. This would, again, be clear and tailored after 
		running the script on the DOORS client for testing.

--------------------------------------------------------------------------------

The DXL script has been implemented to comply to an 80 char maximum per line as
code convention. Comments have been provided when necessary although not 
extensively but only as a way of improving code readibility.
Alternatively, the following could be replace if such rule did not apply to
reduce the required LOC from the overall script:

LOC: 140 - 142
Alternative: if ((attribute1 == filtertext1) && (attribute2 == filtertext2) && attribute3 = filtertext3)) {

LOC: 148 - 149
Alternative: if ((l.attribobjtyp == filtertext1) && (l.attribobjreq == filtertext2)) {

LOC: 155 - 159
Alternative: outfile << numreqs, " o."Object ID ", " o."Object Implementation Status ", linkcount, " o.ObjectText" "\n"

After testing the script with the IBM DOORS client, the following could be better alternatives for the implementation provided:

LOC: 175
Alternatives:
// infoBox("Finished exporting " numreqs " requirements out of " objcount " objects from DOORS Module " fullName(m) "\n")
//export << "Finished exporting " numreqs " requirements out of " objcount " objects from DOORS Module " fullName(m) "\n"
//export << stringOf(dateOf(intOf(today)), "dd  yyyy") "\n"
