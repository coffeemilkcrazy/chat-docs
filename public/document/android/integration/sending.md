# Sending Messages
Once authenticated, users can send and receive messages, which are associated with a specific `CCRoom` object.

CCRoom objects are created by calling `CCRoom.createRoom()`. This method takes a JSONObject of room detail which including members and product.

```java
// Creates and returns a distinct conversation object with the given room detail

CCRoom.createRoom(getRoomDetail(), new CCConstant.CCResultCallback<CCRoom>() {
    @Override
    public void onComplete(CCRoom result, String error) {
    
    }
});
```

Once you have created a room, you are able to send messages as the authenticated user.


The `CCMessage` object represents an individual message within a room. A message within the Chatcafe can consist of one or many pieces of content.


The CCMessage object also declares a convenience method for creating messages with text:
```java
// Creates a message with a string of text.

String messageText = "Hi! How are you";
CCMessage message = new CCMessage.Builder()
        .roomId(ccRoom.getObjectId())
        .text(messageText)
        .build();
                
```

The CCMessage object also declares a convenience method for creating messages with image:
```java
// Creates a message with a bitmap.

CCImage ccImage = CCImage.setBitmap(bitmap);

CCMessage message = new CCMessage.Builder()
        .roomId(ccRoom.getObjectId())
        .image(ccImage)
        .build();
```

## Displaying the conversation
You need to extend `MessageBaseAdapter` as your `ListView`'s adapter

```
//Your listview's adapter
public class MessageAdapter extends MessageBaseAdapter {
...
}
```


In `getView()` method you need to `Override` and set up your own ui elements.

```java
@Override
public View getView(int position, View convertView, ViewGroup viewGroup) {

    ViewHolder holder;

    if (convertView == null) {
        convertView = LayoutInflater.from(activity).inflate(..., viewGroup, false);
        holder = new ViewHolder();
        
        ...
    
        convertView.setTag(holder);
    }else{
        holder = (ViewHolder) convertView.getTag();
    }

    CCMessage message = getItem(position);

    int direction = getDirection(position);

    if (direction == CELL_TYPE_TEXT_DIRECTION_OUTGOING) {
    
    ...
    
    } else if (direction == CELL_TYPE_TEXT_DIRECTION_INCOMING) {
    
    ...
    
    } else if (direction == CELL_TYPE_IMAGE_DIRECTION_OUTGOING) {
    
    ...
    
    } else if (direction == CELL_TYPE_IMAGE_DIRECTION_INCOMING) {
    
    ...
    
    }

    return convertView;
}
```

There is a direction for each message;

* `MessageBaseAdapter.CELL_TYPE_TEXT_DIRECTION_OUTGOING` - The message with text is send from your own device.
* `MessageBaseAdapter.CELL_TYPE_TEXT_DIRECTION_INCOMING` - The message with text is send from other device.
* `MessageBaseAdapter.CELL_TYPE_IMAGE_DIRECTION_OUTGOING` - The message with image is send from your own device.
* `MessageBaseAdapter.CELL_TYPE_IMAGE_DIRECTION_INCOMING` - The message with image is send from other device.


## Recipient Status
ChatCafe allows you the current status of a message for every participant in a conversation. The states are the following:

* `message.sendComplete()` - The message is successfully send or not.
* `message.readCount()` - The message has been "marked as read" by a recipient's device.


Finally setup your adapter as following.

```java

@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);
    ListView messagesList = (ListView) findViewById(...);

    messageAdapter = new MessageAdapter(context, ccRoom);
    messageAdapter.setListView(messagesList);
}


@Override
protected void onResume() {
    messageAdapter.onResume();
    super.onResume();
}

@Override
protected void onPause() {
    messageAdapter.onPause();
    super.onPause();
}
```


## Sending The Message

The CCRoom object is use to send the message:
```java
// Sends the specified message using CCRoom
ccRoom.send(context, message);


// Sends the specified message using adapter
messageAdapter.send(message);

```


That's it, the adapter will do all the work for you!
