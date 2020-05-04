# AngularOnAws
How to deploy an **Angular APP** to **AWS** using `serverless framework` and `@ng-toolkit/serverless`

## Prerequisites
- AWS cli
    - See [AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2.html)
- Angular cli
    - `npm install -g @angular/cli`
- Serverless framework
    - `npm install serverless`
- Create user credentials on AWS 
    - See [AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_users_create.html)

## The process I've followed
- Configure serverless credentials (with custom profile)
    - `serverless config credentials --provider aws --key {KEY} --secret {SECRET} --profile aws-on-aws`
- Create Angular project from cli 
    - `ng new angular-on-aws` (`npm install` run automatically after project creation)
    - `cd angular-on-aws`
- Add serverless plugin
    - `ng add @ng-toolkit/serverless`
- **[FIX]** missing `serverless-api-compression` package in @ng-toolkit/serverless
    - `npm install serverless-api-compression`
- **Customize** configuration `serverless.yml` (`region` and `profile`):
    ```yaml
    provider:
      region: eu-west-3
      profile: angular-on-aws
    ```
- **[FIX]** problem on deploy `TypeError: express is not a function`
    - set to `false` the value of `esModuleInterop` in `tsconfig.json`:
    ```json
    {
      "esModuleInterop": false
    }
    ``` 
- Deploy the project to AWS
    - `npm run build:serverless:deploy`
- Click on the endpoint to see the app online:
    - e.g. `https://{XYZ}.execute-api.{REGION}.amazonaws.com/production`
