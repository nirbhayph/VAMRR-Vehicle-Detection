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
  key:"2812174DB9F279DA3FE3BAADA3D0D31B"
  ...
}
```
Error Messages for Authorization:

```
Invalid Authorization Key
```



