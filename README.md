## Deep Learning based Vehicle Damage Detection

Demo : `https://autodetect.ml`

This is a Deep learning based vehicle damage identification solution. This repository is linked to the React based web application which is integrated with the mentioned system. 

This is a proof of concept for damage detection of vehicles.
Labels that can be detected : `Front` `Rear` `Door` `Fender` `Major-Damage` `Minor-Damage` `Scratches`

The React based web application involves uploading your media file(s), waiting for them to get processed and finally seeing your predicted outputs.

### API Documentation

#### Authorization

Every user is identified by their authorization key. All API requests require authentication from a specific user. For example, seeking sessions for a particular user.

Thus, to authenticate requests, pass your access key in the following format:

```
data {
  key:"<SPECIFY AUTHORIZATION_KEY HERE>"
  ...
}
```
Error Messages for Authorization:

```
Invalid Authorization Key
```
#### Creating and managing sessions

Every time a user wishes to make a new request, they need to specify the sessionId which can take either of the two values:

```
data {
  session:"new"
  ...
}
```
Here, `new` indicates a new sessionId to be created.

If the user wishes to not create a new session, the API allows the option to merge new requests with previous request results by specifying an older sessionId.

```
data {
  session:"9943213153939"
  ...
}
```
#### Retrieving existing sessions

Users can retrieve all sessionIds associated with a key.

`.js example`

```
$(document).ready(function(){
      $.ajax({
      url:'https://autodetect.ml/api/seek/',
      type:'POST',
      data:{
        key:"<SPECIFY AUTHORIZATION_KEY HERE>"
      },
      success:function(result){
      console.log(result);
      }
    });
});
```



