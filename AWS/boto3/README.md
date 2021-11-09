# Python boto3 library


## S3

*Read files and filter by date*

```python
    s3 = boto3.resource('s3')
    my_bucket = s3.Bucket(bucket_name)
    for my_bucket_object in my_bucket.objects.filter(Prefix=path):
        if start_date <= my_bucket_object.last_modified.replace(tzinfo=None) <= end_date:
            print(my_bucket_object.key)
```

