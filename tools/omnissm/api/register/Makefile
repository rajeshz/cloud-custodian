
bucket = c7n-ssm-build
stack = omnissm

deploy:
	GOOS=linux go build -o main register.go
	zip main.zip main
	aws cloudformation package --template-file cfn.yml --s3-bucket $(bucket) --s3-prefix builds --output-template built-template.yml
	aws cloudformation deploy --template-file built-template.yml --stack-name $(stack)
	rm main main.zip built-template.yml

delete:
	aws cloudformation delete-stack --stack-name=$(stack)

update:
	GOOS=linux go build -o main register.go
	zip main.zip main
	aws lambda update-function-code --function-name="omnissm-register" --zip-file fileb://main.zip	
	rm main main.zip


