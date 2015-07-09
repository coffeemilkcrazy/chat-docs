#Authenticate

Once connected, ChatCafe requires every user to be authenticated before they can send and recieve messages. The Authentication process lets you explicitly allow a given user to communicate with other users in `Kaidee` app. A user is defined by Kaidee member ID.

The authentication process starts when you call `openSocket()`.

```java

/*
 * Prepare member data
 * id, privateToken, username
 */

String memberId = ...
String memberPrivateToken = ...
String memberUsername = ...

CCSocket.getInstance().openSocket(memberId, memberUsername, memberPrivateToken, new CCConstant.CCResultCallback<String>() {
    @Override
    public void onComplete(String result, String error) {

    }
});

```

<b>Note:</b> You should authenticate before use others service of this SDK. Normally every times app opening and after user login.

```java
CCSocket.getInstance().disconnect();
```
<b>Note:</b> You should disconnect after app is closing or entering background state also after user logout.
