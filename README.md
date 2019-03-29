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
  key:"<SPECIFY AUTHORIZATION_KEY HERE>",
  ...
}
```

#### Creating and using existing sessions

Every time a user wishes to make a new request, they need to specify the sessionId which can take either of the two values:

```
data {
  session:"new",
  ...
}
```
Here, `new` indicates a new sessionId to be created.

If the user wishes to not create a new session, the API allows the option to merge new requests with previous request results by specifying an older sessionId.

```
data {
  session:"9943213153939",
  ...
}
```
#### Specifying API Endpoints

The `url` attribute can take the following endpoints:

```
url:'https://autodetect.ml/api/request/',
data: {
  ...
}
```
```
url:'https://autodetect.ml/api/lookup/',
data: {
  ...
}
```
```
url:'https://autodetect.ml/api/seek/',
data: {
  ...
}
```

#### Supplying media input to the API /request POST

It is important that the media URL(s) are specified through an array only even if there is only one URL whose output needs to be processed.

`.js example`

```
var url_array = [
    'https://www.autoauctionmall.com/learning-center/contents/uploads/2015/10/damaged-car.jpg?w=100&h=200&k=300',
    'https://www.autoauctionmall.com/learning-center/contents/uploads/2015/10/damaged-car.jpg?w=100&h=200&k=300'
    ];
data: {
  url:url_array,
  ...
}
```

#### POST

All API requests (`/request`, `/lookup`, `/seek`) must have data passed via a POST request ONLY.
```
type:'POST',
data: {
  ...
}
```

#### API /request POST example (Generate JSON output for a request on a new/existing sessionId)

`.js example`

```
var url_array = [
    'https://www.autoauctionmall.com/learning-center/contents/uploads/2015/10/damaged-car.jpg?w=100&h=200&k=300',
    'https://www.autoauctionmall.com/learning-center/contents/uploads/2015/10/damaged-car.jpg?w=100&h=200&k=300',
    'https://www.autoauctionmall.com/learning-center/contents/uploads/2015/10/damaged-car.jpg?w=100&h=200&k=300'
    ];

    $(document).ready(function(){
      $.ajax({
      url:'https://autodetect.ml/api/request/',
      type:'POST',
      data:{
        url:url_array,
        key:"<SPECIFY AUTHORIZATION_KEY HERE>",
        session:"5147839406218"
      },
      success:function(result){
      console.log(result);
      }
    });
});
```

`Sample Output`
```
[
    {
        "sessionId": "4370958592436",
        "fileName": "4679fa55e8c79524212c9b60c8ed59de.json",
        "originalImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/processed\/4679fa55e8c79524212c9b60c8ed59de.jpeg",
        "outputImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4679fa55e8c79524212c9b60c8ed59de.jpeg",
        "visualizationLink": "https:\/\/autodetect.ml\/p.php?p=4370958592436",
        "marker": "{\"label\": \"major-damage\", \"color_rgb_code\": [95.25, 190.5, 127]}, {\"label\": \"front\", \"color_rgb_code\": [254.0, 254.0, 254]}, {\"label\": \"fender\", \"color_rgb_code\": [158.75, 63.5, 127]}, {\"label\": \"minor-damage\", \"color_rgb_code\": [127.0, 254.0, 254]}",
        "textOutputLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4370958592436.txt"
    },
    {
        "sessionId": "4370958592436",
        "fileName": "7d8ccdbf059c96f9bfccf46786ed137d.json",
        "originalImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/processed\/7d8ccdbf059c96f9bfccf46786ed137d.jpeg",
        "outputImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/7d8ccdbf059c96f9bfccf46786ed137d.jpeg",
        "visualizationLink": "https:\/\/autodetect.ml\/p.php?p=4370958592436",
        "marker": "{\"label\": \"major-damage\", \"color_rgb_code\": [95.25, 190.5, 127]}, {\"label\": \"front\", \"color_rgb_code\": [254.0, 254.0, 254]}, {\"label\": \"fender\", \"color_rgb_code\": [158.75, 63.5, 127]}, {\"label\": \"minor-damage\", \"color_rgb_code\": [127.0, 254.0, 254]}",
        "textOutputLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4370958592436.txt"
    },
    {
        "sessionId": "4370958592436",
        "fileName": "94a87f6d2921081b8acd67fe35f3d88c.json",
        "originalImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/processed\/94a87f6d2921081b8acd67fe35f3d88c.jpeg",
        "outputImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/94a87f6d2921081b8acd67fe35f3d88c.jpeg",
        "visualizationLink": "https:\/\/autodetect.ml\/p.php?p=4370958592436",
        "marker": "{\"label\": \"major-damage\", \"color_rgb_code\": [95.25, 190.5, 127]}, {\"label\": \"front\", \"color_rgb_code\": [254.0, 254.0, 254]}, {\"label\": \"fender\", \"color_rgb_code\": [158.75, 63.5, 127]}, {\"label\": \"minor-damage\", \"color_rgb_code\": [127.0, 254.0, 254]}",
        "textOutputLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4370958592436.txt"
    }
]
```

#### Output explanation for /request POST

`sessionId:` The sessionId of the API request (A new one is generated if `new` keyword is specified during /request)
`fileName:` Filename for the `.json` generated
`originalImageLink:` The link for the original image link supplied during API /request
`outputImageLink:` The output image link pointing to the labeled image
`visualizationLink:` The link to view the entire session via a browser
`marker:` The label specification for the generated output image, along with color coding for each label
`textOutputLink:` The link to the text output specifying processing details for a /request made

#### API /lookup POST example (Retrieve existing sessionId's data)

`.js example`

```
$(document).ready(function(){
      $.ajax({
      url:'https://autodetect.ml/api/lookup/',
      type:'POST',
      data:{
        key:"<SPECIFY AUTHORIZATION_KEY HERE>",
        session:"5147839406218"
      },
      success:function(result){
      console.log(result);
      }
    });
});
```

`Sample Output`
```
[
    {
        "sessionId": "4370958592436",
        "fileName": "4679fa55e8c79524212c9b60c8ed59de.json",
        "originalImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/processed\/4679fa55e8c79524212c9b60c8ed59de.jpeg",
        "outputImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4679fa55e8c79524212c9b60c8ed59de.jpeg",
        "visualizationLink": "https:\/\/autodetect.ml\/p.php?p=4370958592436",
        "marker": "{\"label\": \"major-damage\", \"color_rgb_code\": [95.25, 190.5, 127]}, {\"label\": \"front\", \"color_rgb_code\": [254.0, 254.0, 254]}, {\"label\": \"fender\", \"color_rgb_code\": [158.75, 63.5, 127]}, {\"label\": \"minor-damage\", \"color_rgb_code\": [127.0, 254.0, 254]}",
        "textOutputLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4370958592436.txt"
    },
    {
        "sessionId": "4370958592436",
        "fileName": "7d8ccdbf059c96f9bfccf46786ed137d.json",
        "originalImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/processed\/7d8ccdbf059c96f9bfccf46786ed137d.jpeg",
        "outputImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/7d8ccdbf059c96f9bfccf46786ed137d.jpeg",
        "visualizationLink": "https:\/\/autodetect.ml\/p.php?p=4370958592436",
        "marker": "{\"label\": \"major-damage\", \"color_rgb_code\": [95.25, 190.5, 127]}, {\"label\": \"front\", \"color_rgb_code\": [254.0, 254.0, 254]}, {\"label\": \"fender\", \"color_rgb_code\": [158.75, 63.5, 127]}, {\"label\": \"minor-damage\", \"color_rgb_code\": [127.0, 254.0, 254]}",
        "textOutputLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4370958592436.txt"
    },
    {
        "sessionId": "4370958592436",
        "fileName": "94a87f6d2921081b8acd67fe35f3d88c.json",
        "originalImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/processed\/94a87f6d2921081b8acd67fe35f3d88c.jpeg",
        "outputImageLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/94a87f6d2921081b8acd67fe35f3d88c.jpeg",
        "visualizationLink": "https:\/\/autodetect.ml\/p.php?p=4370958592436",
        "marker": "{\"label\": \"major-damage\", \"color_rgb_code\": [95.25, 190.5, 127]}, {\"label\": \"front\", \"color_rgb_code\": [254.0, 254.0, 254]}, {\"label\": \"fender\", \"color_rgb_code\": [158.75, 63.5, 127]}, {\"label\": \"minor-damage\", \"color_rgb_code\": [127.0, 254.0, 254]}",
        "textOutputLink": "https:\/\/autodetect.ml\/file_handler\/uploads\/4370958592436\/out\/4370958592436.txt"
    }
]
```

#### API /seek POST example (Retrieving existing sessionIds)

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

`Sample Output`
```
[
    {
        "sessionId": "11299504729248",
        "lastModifiedTime": "2019-03-29 05:28:17.884912910"
    },
    {
        "sessionId": "5147839406218",
        "lastModifiedTime": "2019-03-29 05:29:07.881948821"
    },
    {
        "sessionId": "6112784572874",
        "lastModifiedTime": "2019-03-29 04:40:23.874150987"
    }
]
```

#### Error Messages

If you encounter any of the following messages, you may have not specified the url/data attributes in the valid format.

```
Invalid Authorization Key

Session Does Not Exist

Post data not found!

No sessions found

Redundant Process Request

Unauthorized Access

Invalid Media Format (.png, .jpeg, .jpg only)*

Invalid Format for Data Provided, (There may possibly be a problem with the Media URL)

Please check your post data!

Invalid Header Contents

Media URLs not passed!
```
NOTE: If you encounter any other problems, feel free to open an issue.

Authors:
(@nirbhayph), (@dhirensc)

VAMRR Technologies Pvt. Ltd.
