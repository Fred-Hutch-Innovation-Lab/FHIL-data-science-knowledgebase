# AWS

[AWS at FH](https://sciwiki.fredhutch.org/scicomputing/store_objectstore/)
[AWS Command Line Interface (CLI)](https://aws.amazon.com/s3/)
[AWS S3 commands](https://docs.aws.amazon.com/cli/latest/reference/s3/index.html)


File storage in AWS is cheaper than the fast drive, but may be less accessible for quick use. AWS storage also allows secure file transfers to external collaborators.

[Motuz](https://motuz.fredhutch.org/login) is an in-house tool for transfering files from FH drives to AWS. 

S3 storage has innate version tracking and trash buffer. From the FH wiki:
```
Data stored in managed S3 buckets are not backed up in the traditional sense, but rather versioned:
if a new version of a file is uploaded, the older version is saved in S3.
Similarly, if data is deleted, the versions aren’t and can be retrieved for up to 60 days.
```

# Basic commands

## Copying files

copy the file hello.txt from your current directory to the top-level folder of an S3 bucket

`aws s3 cp hello.txt s3://fh-pi-doe-j-eco/`

Copy the file hello.txt to the folder path a/b/c and folder are not created in advance.
`aws s3 cp s3://fh-pi-doe-j-eco/hello.txt s3://fh-pi-doe-j-eco/a/b/c/`
Without the trailing /, the file hello.txt will be copied into the S3 bucket under the filename 'c', rather than into the desired prefix itself.

Copying files from an S3 bucket to the machine you are logged into, the current directory on the (rhino or gizmo) , represented by dot (.) in here:
`aws s3 cp s3://fh-pi-doe-j-eco/hello.txt .`

## Listing files

list the contents of your lab’s bucket:
`aws s3 ls s3://fh-pi-doe-j-eco/`

To list the contents of a specific folder, just add the folder path to the end of the previous example:

`aws s3 ls s3://fh-pi-doe-j-eco/a/b/c/`

See the entire contents of every folder in your bucket:
`aws s3 ls --recursive --summarize s3://fh-pi-doe-j-eco/`
You can optionally add the --human-readable argument to that command to get the file sizes output in a more easily recognizable format. This is roughly equivalent to the command ls -alhR /path/on/posix/filesystem when working on a posix file system in a shell such as Bash.

## Accessing buckets from other labs

Working with a bucket that belongs to another lab, you will need to ensure that you set the object ACL (access control list) correctly when uploading data into that other lab’s bucket:
To do this, append the argument --acl bucket-owner-full-control to the aws s3 cp or aws s3 sync commands. If you are using Motuz to copy data, Motuz will handle this for you.

aws s3 cp --acl bucket-owner-full-control s3://fh-pi-doe-j-eco/test.txt s3://fh-pi-heisenberg-w-eco/

