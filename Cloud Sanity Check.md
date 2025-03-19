# Cloud Sanity Check

!!!!!insert image desc!!!!!!!!


login the given crednetials
```
┌──(kali㉿kali)-[~]
└─$ aws configure
AWS Access Key ID [None]: *********5Z7UW
AWS Secret Access Key [None]: ****************************QHar
Default region name [None]: us-west-2
Default output format [None]: 
```
commands:
test
```
┌──(kali㉿kali)-[~]
└─$ aws s3 ls --region us-west-2

An error occurred (AccessDenied) when calling the ListBuckets operation: User: arn:aws:iam::332173347248:user/user0 is not
authorized to perform: s3:ListAllMyBuckets because no identity-based policy allows the s3:ListAllMyBuckets action

```
not working
tried this command also the path
```
┌──(kali㉿kali)-[~]
└─$ aws ssm get-parameters-by-path --path "/" --region us-west-2

An error occurred (AccessDeniedException) when calling the GetParametersByPath operation: User: arn:aws:iam::332173347248:user/user0 is not authorized to perform: ssm:GetParametersByPath on resource: arn:aws:ssm:us-west-2:332173347248:parameter/ because no identity-based policy allows the ssm:GetParametersByPath action

```
but here is the command that worked
```
                                                                                                                    
┌──(kali㉿kali)-[~]
└─$ aws secretsmanager list-secrets --region us-west-2
{
    "SecretList": [
        {
            "ARN": "arn:aws:secretsmanager:us-west-2:332173347248:secret:secret-flag-Im0H0Z",
            "Name": "secret-flag",
            "LastChangedDate": "2025-03-17T03:15:42.026000-04:00",
            "LastAccessedDate": "2025-03-18T20:00:00-04:00",
            "Tags": [],
            "SecretVersionsToStages": {
                "a007a97d-73c7-430d-879f-e9cc72013f6a": [
                    "AWSCURRENT"
                ]
            },
            "CreatedDate": "2025-03-17T03:15:41.704000-04:00"
        }
    ]
}
```
and get the "Name" Header
```
┌──(kali㉿kali)-[~]
└─$ aws secretsmanager get-secret-value --secret-id "secret-flag" --region us-west-2
{
    "ARN": "arn:aws:secretsmanager:us-west-2:332173347248:secret:secret-flag-Im0H0Z",
    "Name": "secret-flag",
    "VersionId": "a007a97d-73c7-430d-879f-e9cc72013f6a",
    "SecretString": "{\"flag\":\"THM{for_your_eyes_only}\"}",
    "VersionStages": [
        "AWSCURRENT"
    ],
    "CreatedDate": "2025-03-17T03:15:42.022000-04:00"
}
```
THM{for_your_eyes_only}
