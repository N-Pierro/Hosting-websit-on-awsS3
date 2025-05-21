# Task outline 

|  Task           | Description                                                     |
|-----------------|-----------------------------------------------------------------|
| Task 1          |Creating a bucket                                              |  
| Task 2         |Upload website content to bucket                                  |
| Task3     | Configure static-website on Amazon S3                                 |
| Task 4   |Make Object in the s3 bucket public                                      



## Task 1

- Log into the `AWS console`

- Access Amazon S3 from your AWS Management console. `Keep note of the region in which you want your bucket to be created in by switching to the appropriate region before creating the bucket`

- Create a bucket and give it a name.

- Enable ACLs and Bucket Versioning


## Task 2

- On the Management consol search and open the s3 bucket service

- Locate the s3 bucket created above. This will look like this [s3 bucket]()

- Upload the 2 files in the webfiles directory of this project using the [link]()

- This should look like this when your done 

|![upload:status]()  |
|--------------------|
|S3 service Management consol|


## Task 3

- Select the properties section of the bucket and scroll down to `static website hosting` 

- Click on edit, to enable static website hosting. By default it is disable. This should like this. 

![static-hosting]()

- Head back to the previes page below the `static website hosting` and copy the generated url for the static website

- Click on this url. You should see a 403 error message 

![403Error]()



## Task 4

- The reason for the 403 error is a result of the objects in this bucket not being accessible 

- To fix this;
    - Go the bucket 
    - Select the objects within the bucket, here is where the ACL described above is used

    - Make this objects public by clicking on actions then `make public using ACL`

    - Confirm and save 

    ![makePublic]()

- One more thing to edit. `Block Public Access Settings`

- AWS blocks public access by default. You need to disable this at the  bucket level:

    - Go to Permissions tab

    - Click Block public access (bucket settings)

    - Uncheck "Block all public access"

    - Confirm and save

- If the 403 error message still persist, update the bucket policy
    - Go to Permissions tab

    - Scroll to Bucket Policy

    - Paste the policy above (update the bucket name)

    ```json
    {
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*"
             }
        ]
    }
    ```

    - Save

This should solve the 403 error issue and the website is successfully hosted. 