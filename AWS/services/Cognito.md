# Amazon Cognito
認証基盤
```
// Amazon Cognito 認証情報プロバイダーを初期化します
AWS.config.region = 'ap-northeast-1'; // リージョン
AWS.config.credentials = new AWS.CognitoIdentityCredentials({
    IdentityPoolId: 'ap-northeast-1:6028e4f8-5380-457e-b802-5f6be5abf66f', #=> 認証のID的な
});
```

## IDプール
