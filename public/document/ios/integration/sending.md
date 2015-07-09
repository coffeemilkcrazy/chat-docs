# Sending Messages
Once authenticated, users can send and receive messages, which are associated with a specific room object.

## CCRoom
[CCRoom](https://github.com/dealfish/iOSDealFishMobile/blob/feature/chat_client/ExternalFrameworks/ChatSocket/CCRoom%2BAddition.h) objects are created by calling
 `createRoomWithBuyer:seller:product:` on [CCRoom](https://github.com/dealfish/iOSDealFishMobile/blob/feature/chat_client/ExternalFrameworks/ChatSocket/CCRoom%2BAddition.h). Room are set to be distinct, which ensures that there is only one unique conversation between the given buyer, seller and product.

* `buyer` - `NSDictionary` of buyer detail.
* `seller` - `NSDictionary` of seller detail.
* `product` - `NSDictionary` of product detail.

```objectivec
// Creates and returns a CCRoom object
[CCRoom createRoomWithBuyer:buyer seller:seller product:product completionBlock:^(CCRoom *room, NSError *error) {
        if (room) {
            // Creates room success
        }
    }];
```

## CCMessage

The [CCMessage](https://github.com/dealfish/iOSDealFishMobile/blob/feature/chat_client/ExternalFrameworks/ChatSocket/CCMessage%2BAddition.h) object represents an individual message within a conversation.

[CCMessage](https://github.com/dealfish/iOSDealFishMobile/blob/feature/chat_client/ExternalFrameworks/ChatSocket/CCMessage%2BAddition.h) objects are initialized by calling `createMessageText:image:` on [CCMessage](https://github.com/dealfish/iOSDealFishMobile/blob/feature/chat_client/ExternalFrameworks/ChatSocket/CCMessage%2BAddition.h). This creates an [CCMessage](https://github.com/dealfish/iOSDealFishMobile/blob/feature/chat_client/ExternalFrameworks/ChatSocket/CCMessage%2BAddition.h) object that is ready to be sent. The initialization variables are the following:

* `text` - A message to be sent.
* `image` - An optional image.

```objectivec
// Creates and returns a new CCMessage object
CCMessage *message = [CCMessage createMessageText:text image:image];
```

## Sending The Message
Once an [CCMessage](https://github.com/dealfish/iOSDealFishMobile/blob/feature/chat_client/ExternalFrameworks/ChatSocket/CCMessage%2BAddition.h) object is initialized, it is ready to be sent. The message is sent by calling `sendMessage:progress:completionBlock:` on `CCRoom`.

```objectivec
//Sends the specified message
[room sendMessage:messageObj progress:^(int percentDone) {
    // Upload image progress.
  }
  completionBlock:^(CCMessage *message, NSError *error) {
    // Send message complete.
    NSLog("send message: %@",message);
}];

```

## Receiving Message
Once message is sent, the recipient can receive the message by set delegate Blah blah blah.
```objectivec
[[CCSocket shareInstance] setDelegate:self];
```
