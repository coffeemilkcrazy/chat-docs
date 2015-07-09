#Authenticate

Once connected, ChatCafe requires every user to be authenticated before they can send and recieve messages. The Authentication process lets you explicitly allow a given user to communicate with other users in `Kaidee` app. A user is defined by Kaidee member ID.

The authentication process starts when you call `openSocketWithUserID:privateToken:username:completionBlock:`.

```objective-c

/*
 * Prepare member data
 * id, privateToken, username
 */

NSString *memberId = ...
NSString *memberPrivateToken = ...
NSString *memberUsername = ...

[[CCSocket shareInstance] openSocketWithUserID:memberId privateToken:memberPrivateToken username:memberUsername completionBlock:^(BOOL success, NSString *user_id, NSError *error) {
    if (success){
        // Authentication success.
    }
    else{
        // Authentication fail.
    }
}];

```

<b>Note:</b> You should authenticate before use others service of this SDK. Normally every times app opening and after user login.

```objective-c
[[CCSocket shareInstance] disconnect];
```
<b>Note:</b> You should disconnect after app is closing or entering background state also after user logout.
