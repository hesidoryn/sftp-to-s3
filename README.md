# sftp-to-s3

Docker image which provides an SFTP access to a specified S3 bucket.

## Usage

Pull the image from docker hub repository 

    docker pull hesidoryn/sftp-to-s3

Run the container with 

<pre>
    docker run \
    	-e SFTP_USER=user \
    	-e SFTP_PASSWORD=pass \
    	-e AWS_ACCESS_KEY_ID=access_key \
    	-e AWS_SECRET_ACCESS_KEY=secret_key \
    	-e S3_BUCKET=bucket \
    	-e S3_KEY=/key \
    	--privileged \
		-p 222:22 \
		-d \
    	hesidoryn/sftp-to-s3 
</pre>

You have to specify the AWS credentials via `AWS_ACCESS_KEY_ID `and `AWS_SECRET_ACCESS_KEY`.
You have also to specify the bucket (and the key) to mount via `S3_BUCKET` and `S3_KEY` (the key should start with a slash `/`). 
 
Now you can try to login via `sftp` using the username specified in `SFTP_USER` and the password specified in `SFTP_PASSWORD`.
 
    $ sftp -P 222 user@localhost
    user@localhost's password:
    Connected to localhost.


## Optional server-side encryption using KMS

You can specify optional environment variable `KMS_KEY_ID` for server-side encrtption.
<pre>
 docker run \
    	-e SFTP_USER=user \
    	-e SFTP_PASSWORD=pass \
    	-e AWS_ACCESS_KEY_ID=access_key \
    	-e AWS_SECRET_ACCESS_KEY=secret_key \
    	-e S3_BUCKET=bucket \
    	-e S3_KEY=/key \
        <b>-e KMS_KEY_ID=kms_key</b> \
    	--privileged \
		-p 222:22 \
		-d \
    	hesidoryn/sftp-to-s3
</pre>
Note that KMS Key should be created in bucket region.
