## Setting aws-nuke on Window

> **참고** <br>
https://github.com/rebuy-de/aws-nuke/releases <br>
https://docs.aws.amazon.com/ko_kr/cli/latest/userguide/getting-started-install.html

<br>

1. https://github.com/rebuy-de/aws-nuke/releases에 접근 후 window.zip을 다운로드 한다.
<img width="1127" height="405" alt="Image" src="https://github.com/user-attachments/assets/1283247e-1bb9-4e73-8bdc-6d39aee5346c" />

<br>

2. 해당 zip 파일을 압축을 푼 후 이름을 aws-nuke로 이름을 변경한다.
<img width="782" height="141" alt="Image" src="https://github.com/user-attachments/assets/7af1da19-4dac-4221-9d80-e93672af7312" />

<br>

3. aws nuke를 C:\Windows\System32 경로에 넣는다.

<br>

4. IAM User를 생성한 뒤, AdministratorAccess 권한을 부여하고, 이후 Access Key를 발급한다.

<br>

5. AWSCLIv2를 설치한다.
<img width="969" height="274" alt="Image" src="https://github.com/user-attachments/assets/8865d672-41f9-4758-9a53-f8b015e57a69" />

<br>

6. PowerShell을 관리자 권한으로 실행한다.

<br>

7. aws configure을 설정한다.
<img width="874" height="218" alt="Image" src="https://github.com/user-attachments/assets/f33798dd-31ba-43ef-9627-01e97533ba5c" />

<br>

8. C:\Users\user경로로 이동한다.
```powershell
cd ~
```

<br>

9. 메모장에 아래와 값은 값을 입력 후 <ACCOUNT_ID>를 본인이 사용하는 AWS Account ID로 변경한다.
```powershell
notepad config.yml
```

```yaml
regions:
- global

account-blacklist:
- "999999999999"

resource-types:
  excludes:
  - IAMUser
  - IAMUserPolicyAttachment
  - IAMUserAccessKey
  - Route53HostedZone
  - OSPackage

accounts:
 <ACCOUNT_ID>: {}
```

<br>

10. 아래 명령어를 입력 후 자기의 AWS Account ID랑 맞는지 확인한다.
```powershell
aws sts get-caller-identity --query 'Account' --output text
```

<br>

11. aws-nuke를 실행시킨다.
```powershell
aws-nuke -c config.yml --no-dry-run
```