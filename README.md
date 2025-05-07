SDA2014

MERN Stack Blog App Deployment – Implementation Summary

	1.	MongoDB Atlas Setup:

	•	Created a free-tier MongoDB Atlas cluster.
	•	Added EC2 IP to the network access list.
	•	Created a database user and copied the connection string.
	•	Added the connection string to the backend .env file under MONGODB.

*******************************************************************
	2.	Frontend Hosting on S3:

	•	Created an S3 bucket named yourname-blogapp-frontend in region eu-north-1.
	•	Unchecked “Block all public access” and enabled static website hosting.
	•	Applied a public bucket policy to allow access to all objects.
	•	Built the React frontend using pnpm run build.
	•	Deployed the dist/ folder to the bucket using aws s3 sync.
**************************************************************************
	3.	Media Upload Bucket (S3):
	•	Created a second bucket named yourname-blogapp-media.
	•	Disabled all public access.
	•	Added the required CORS policy to allow frontend to upload files.
	•	Tested file upload by manually uploading a test file and accessing its URL.
****************************************************************************************
	4.	IAM User and Permissions:
	•	Created a new IAM user with programmatic access.
	•	Attached a custom policy to allow full access to the *-media bucket.
	•	Added the AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY to backend .env.
**************************************************************************************************
	5.	Backend Deployment on EC2:
	•	Launched a free-tier EC2 instance with Ubuntu.
	•	Installed Node.js (via NVM), PM2, and AWS CLI.
	•	Cloned the MERN app repository to /home/ubuntu/blog-app.
	•	Created .env file in /backend directory with all required configs (MongoDB, S3, JWT).
	•	Installed dependencies and started the server with PM2.
	•	Enabled PM2 to auto-start on system reboot.
******************************************************************************************************
	6.	Frontend Configuration:
	•	In /frontend, created .env file with VITE_BASE_URL pointing to EC2 Public DNS and VITE_MEDIA_BASE_URL pointing to media bucket.
	•	Installed dependencies and built the frontend.
	•	Synced the build to S3 as in Step 2.
***********************************************************************
	7.	Testing and Validation:
	•	Verified S3 static site loads correctly (frontend).
	•	Used curl -I to confirm HTTP 200 OK from frontend S3 URL.
	•	Confirmed media files upload successfully and are publicly accessible.
	•	Tested blog creation and media attachment functionality.

