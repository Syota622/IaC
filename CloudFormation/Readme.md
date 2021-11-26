# CloudFormationテンプレートの保管するためのS3バケットを作成
aws cloudformation create-stack --stack-name cfn-template-s3-store --template-body file://cloudformatin-template-s3-store.yml --parameters ParameterKey=CloudFormationTemplateBucketName,ParameterValue=cloudformatin-template-s3-store ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

## aws cli cloudformation create-stack
aws cloudformation create-stack --stack-name server --template-body file://Server/root-server.yml \
  --parameters ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

## aws cli cloudformation update-stack
aws cloudformation update-stack --stack-name server --template-body file://Server/root-server.yml \
  --parameters ParameterKey=ProjectName,ParameterValue=suzukis ParameterKey=Environment,ParameterValue=prod

## S3 アップロード
aws s3 cp ~/Desktop/IaC/CloudFormation s3://suzukis-cloudformatin-template-s3-store-prod --recursive

## aws cli cloudformation package
aws cloudformation package --template-file ./NW/root-network.yml \
	--s3-bucket suzukis-cloudformatin-template-s3-store-prod \
	--output-template-file ./NW/package/packaged.yml

## aws cli cloudformation deploy
aws cloudformation deploy --template-file /Users/shota/Desktop/IaC/CloudFormation/NW/package/packaged.yml \
  --stack-name suzukis-network --parameter-overrides ProjectName=suzukis Environment=prod IsCreateNATGatewayA=false \
	IsCreateNATGatewayC=false IsCreateNATGatewayD=false

## ROLLBACK_COMPLETE 削除
aws cloudformation 

## Git操作 マージ
$ git checkout main
$ git merge ${branch}
$ git push
