Docker image tag:

815015007739.dkr.ecr.eu-west-1.amazonaws.com/mythicalmysfits/service:latest


{
    "repository": {
        "repositoryArn": "arn:aws:ecr:eu-west-1:815015007739:repository/mythicalmysfits/service",
        "registryId": "815015007739",
        "repositoryName": "mythicalmysfits/service",
        "repositoryUri": "815015007739.dkr.ecr.eu-west-1.amazonaws.com/mythicalmysfits/service",
        "createdAt": 1586767969.0,
        "imageTagMutability": "MUTABLE",
        "imageScanningConfiguration": {
            "scanOnPush": false
        }
    }
}

aws ecr describe-images --repository-name mythicalmysfits/service
{
    "imageDetails": [
        {
            "registryId": "815015007739",
            "repositoryName": "mythicalmysfits/service",
            "imageDigest": "sha256:b0673693acb5332aa23b854df2b920c4be3fd7d983c06e3f36bb094cffea65e5",
            "imageTags": [
                "latest"
            ],
            "imageSizeInBytes": 202641097,
            "imagePushedAt": 1586768283.0
        }
    ]
}


aws elbv2 create-load-balancer --name mysfits-nlb --scheme internet-facing --type network --subnets subnet-06162cecd4f73001e subnet-0e8acfd8c2684cc07 > ~/environment/nlb-output.json


aws elbv2 create-target-group --name MythicalMysfits-TargetGroup --port 8080 --protocol TCP --target-type ip --vpc-id vpc-0b167b0c1585f0d78 --health-check-interval-seconds 10 --health-check-path / --health-check-protocol HTTP --healthy-threshold-count 3 --unhealthy-threshold-count 3 > ~/environment/target-group-output.json


aws elbv2 create-listener --default-actions TargetGroupArn=arn:aws:elasticloadbalancing:eu-west-1:815015007739:targetgroup/MythicalMysfits-TargetGroup/b9cdeed4b9a4c2f0,Type=forward --load-balancer-arn arn:aws:elasticloadbalancing:eu-west-1:815015007739:loadbalancer/net/mysfits-nlb/42f4a33b896d2ad7 --port 80 --protocol TCP


http://mysfits-nlb-123456789-abc123456.elb.us-east-1.amazonaws.com/mysfits
http://mysfits-nlb-42f4a33b896d2ad7.elb.eu-west-1.amazonaws.com/mysfits
http://mysfits-nlb-42f4a33b896d2ad7.elb.eu-west-1.amazonaws.com/mysfits