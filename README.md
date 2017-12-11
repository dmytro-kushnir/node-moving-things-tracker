# node-tracker-by-detections

Realtime tracker by detections wrote in javascript for node.js / browsers

### Introduction

node-tracker-by-detections is a javascript implementation of the _"tracker by detections"_ for realtime multiple object tracking (MOT).

It takes in input a txt file _(TODO change to json)_ generated by [node-yolo](https://github.com/moovel/node-yolo) and outputs a `tracker.json` file that assigns unique IDs to the YOLO detections bbox.

_The detections entry file could be generated by other neural network / algorithm than YOLO, it just needs to respects the format specified in #input blabla link_ 


**Detections input:**

![detections](https://user-images.githubusercontent.com/533590/33817459-030e3822-de40-11e7-979d-0c8071ea2a94.gif)

**Tracker output:**

![tracker](https://user-images.githubusercontent.com/533590/33817550-6913047c-de40-11e7-8552-f284c738f1c0.gif)


### Installation and usage

> Requires node.js , available as a npm module: http://npmjs.com/node-tracker-by-detections

```bash
# Install globaly to use as command line tool
npm install -g node-tracker-by-detections 

# Install localy your node.js / javascript project
npm install --save node-tracker-by-detections 
```

**Command line usage**

> NOTE : for now customized for the use case of [lab-beat-the-traffic](https://github.com/moovel/lab-beat-the-traffic)

```bash
node-tracker-by-detections PATH_TO_YOLO_DETECTIONS.txt
# This will output a tracker.json file in the same folder containing the tracker data
```

**As an external module**

> See usage in [lab-traffic-cam](https://github.com/moovel/lab-traffic-cam/blob/master/server/counter/Counter.js#L57)

```javascript
const Tracker = require('node-tracker-by-detections').Tracker;

Tracker.updateTrackedItemsWithNewFrame(detectionScaledOfThisFrame, currentFrame);

const trackerDataForThisFrame = Tracker.getJSONOfTrackedItems();
```

### Detections Input and tracker output format

**Detections Input**

rawdetections.txt

```json
{"frame":0,"detections":[{"x":699,"y":99,"w":32,"h":19,"prob":34,"name":"car"},{"x":285,"y":170,"w":40,"h":32,"prob":26,"name":"car"},{"x":259,"y":178,"w":75,"h":46,"prob":42,"name":"car"},{"x":39,"y":222,"w":91,"h":52,"prob":61,"name":"car"},{"x":148,"y":199,"w":123,"h":55,"prob":53,"name":"car"}]}
{"frame":1,"detections":[{"x":699,"y":99,"w":32,"h":19,"prob":31,"name":"car"},{"x":694,"y":116,"w":34,"h":23,"prob":25,"name":"car"},{"x":285,"y":170,"w":40,"h":32,"prob":27,"name":"car"},{"x":259,"y":178,"w":75,"h":46,"prob":42,"name":"car"},{"x":39,"y":222,"w":91,"h":52,"prob":61,"name":"car"},{"x":148,"y":199,"w":123,"h":55,"prob":52,"name":"car"}]}
```

**Tracker Output**

```javascript
{
  // Tracker data for each frame
  "43": [
    {
      "id": "900e36a2-cbc7-427c-83a9-819d072391f0",
      "idDisplay": 0,
      "x": 628,
      "y": 144,
      "w": 48,
      "h": 29,
      "name": "car",
      "isZombie": false,
      "zombieOpacity": 1,
      "appearFrame": 35,
      "disappearFrame": null
    },
    {
      "id": "38939c38-c977-40a9-ad6a-3bb916c37fa1",
      "idDisplay": 1,
      "x": 620,
      "y": 154,
      "w": 50,
      "h": 35,
      "name": "car",
      "isZombie": false,
      "zombieOpacity": 1,
      "appearFrame": 43,
      "disappearFrame": null
    }
  ]
  ...
  // General info about each tracked item
  "general": [{
      "id": "a706f0c1-db07-4f93-834a-43d18267b16e",
      "idDisplay": 102,
      "appearFrame": 1301,
      "disappearFrame": 1302,
      "disappearArea": {
        "x": 512,
        "y": 193
      },
      "nbActiveFrame": 1
    },
    {
      "id": "374b9ffd-46ff-490e-b994-f78e17517414",
      "idDisplay": 95,
      "appearFrame": 1219,
      "disappearFrame": 1315,
      "disappearArea": {
        "x": 21,
        "y": 551
      },
      "nbActiveFrame": 96
    }]
}
```

### Editor to define "active areas"

> TODO


### API docs 

> TODO

### Limitations

No params tweaking is possible via command-line for now, it is currently optimized for car tracking, and many improvements are [still to be implemented](https://github.com/tdurand/node-tracker-by-detections/issues/2).

