Hi Ed,

Here is the demo of what Studio Hub would run on their Web Server to access the Image Previews at run time.

That is assuming that they do that and not store them on their server, as what appears to be their current plan.

----------------

Aspen Image Preview Service URL and Virtual Directory

https://hal.umusic.com/AspenImagePreviewService 

domain\user (aka Username):
s224951-umg\ImgSrcUser

password:
4vdupxpW4FvX5S7J

Studio Hub Unique AssetOwnerId:
0C305EC9-4AF4-466F-B0E4-8CA35F6F2D05

Thanks,
Dave

--------------------------------
--------------------------------

Hi Ed,

Instructions and requests:

What I need from you (maybe):
-	JB tells me that the firewall should already be set up to let your servers hit the Aspen Image Preview Service.

In the attached demo, put the above mentioned items here in the indicated spots.
	Look for:
-	{AssetOwnerId goes here}
-	{Username goes here}
-	{Password goes here} 

Also, substitute the staging URL with the production one provided above.

Aspen IPS Usage notes:

Client-side:
-	Use image tags (<img>) with your Same Origin Proxy URL as the “src”
		Example:  
			<img src="/api/Proxy/14941E49-AD21-458E-A9C0-6F89B9A69936" alt="Sample Image Preview in Aspen Staging" style="max-height: 250px; max-width: 250px;" />
-	Use either css classes or style attributes in the image tag and set the “max-height” and “max-width” to limit the size proportionally to whatever size you want
		Example: 
			style="max-height: 250px; max-width: 250px;"
-	The reason for this is that Atalasoft has a bug where, at times, it will not honor the requested height/width for a very thin or very tall images during the Image Preview Generation process.
		This is not an issue if you put the above constraints on all your image tags
		The above style has been test successfully with IE9, and current versions of Chrome and Firefox

Server-side:
-	Create the actual call to IPS with the following format:
		https://{AspenServerUrl}/AspenImagePreviewService/DamsImagePreview/{ PreviewAssetId}?ao={AssetOwnerId}
			The AssetOwnerId (a guid) is supplied to you above
				If this guid is not passed to us, you will not have access to your Private or Restricted asset previews
				This is part of the Access Control requirements, as you know	
-	Create an “Authorization Header” using Base64 encoding (see the demo)
		Use the credentials supplied above
-	None of the above credentials or the Asset Owner ID may ever leave your server(s), and proper security must be in place on the server(s)
		This goes without saying, but I am obliged to state it directly
-	The demo shows how to set/capture the appropriate headers, status code (on success and failure), and how to re-output the image to your client-side image tags.
		Please note the special handling of the cache-control header


To keep this short, please refer to the code for any other questions you or your developers may have.
If you or your developers still have questions, I will do my best to answer them.

Thanks,
Dave

