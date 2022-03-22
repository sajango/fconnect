```
aws cloudformation create-stack --stack-name vpc --template-body file://infra/vpc/vpc-3azs.yaml --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name alert --template-body file://infra/operations/alert.yaml --parameters ParameterKey=Email,ParameterValue=sangnd.it@gmail.com --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name waf --template-body file://infra/security/waf.yaml --parameters ParameterKey=Scope,ParameterValue=REGIONAL ParameterKey=RateLimit,ParameterValue=100 ParameterKey=BotControlEffect,ParameterValue=Block ParameterKey=ReputationListEffect,ParameterValue=Disable ParameterKey=BotControlEffect,ParameterValue=Disable --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name zone-public --template-body file://infra/vpc/zone-public.yaml --parameters ParameterKey=Name,ParameterValue=sangamele.net --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name client-sg --template-body file://infra/vpc/client-sg.yaml --parameters ParameterKey=ParentVPCStack,ParameterValue=vpc --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name secret --template-body file://infra/state/secretsmanager-dbsecret.yaml --parameters --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name rds-mysql --template-body file://infra/state/rds-mysql.yaml --parameters ParameterKey=ParentVPCStack,ParameterValue=vpc ParameterKey=ParentClientStack,ParameterValue=client-sg ParameterKey=ParentAlertStack,ParameterValue=alert ParameterKey=ParentSecretStack,ParameterValue=secret ParameterKey=DBInstanceIdentifier,ParameterValue=dspstaging --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name elasticache-redis --template-body file://infra/state/elasticache-redis.yaml --parameters ParameterKey=ParentVPCStack,ParameterValue=vpc ParameterKey=ParentClientStack,ParameterValue=client-sg ParameterKey=ParentAlertStack,ParameterValue=alert --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name fargate-cluster --template-body file://infra/fargate/cluster.yaml --parameters ParameterKey=ParentVPCStack,ParameterValue=vpc --region ap-southeast-1 --profile sangnddev

aws cloudformation create-stack --stack-name fargate-service --template-body file://infra/fargate/service-cluster-alb.yaml --parameters ParameterKey=ParentVPCStack,ParameterValue=vpc --region ap-southeast-1 --profile sangnddev
```


