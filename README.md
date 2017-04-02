# place-peer-hivemind

console pastable javascript to manage a fleet of subscribers given a leader's selected bitmap image for /r/place

this is meant to coordinate many willing participants in a common drawing of a given leader's loaded bitmap image.

https://www.reddit.com/r/place/comments/62y0pn/hivemind_slave_peering_javascript_injection/

## TODO

- Finish adding Hex -> picker ID switch: https://github.com/bioshazard/place-peer-hivemind/blob/master/peerjsleader.js#L118
- Maybe add an interface for x/y offset configuration
- Maybe change who you subscribe to in interface for slave
- More stats for leader for current campaign on the draggable pane
- Find a good way to include peerjs.min.js. Maybe host it on my peer broker server?
- Clean this up to not look like a sketchy nightmare.

## Usage

Go to reddit.com/r/place and the one of the following:

## Leader

If you want to be a leader, open the peerjsleader.js file 

Change the `var leaderId = 'leader';` at the top of the file to something unique your subscribers can use (eg, 'thebluecorner')

Copy/paste the content into your developer console (F12), hit enter. This will load the PeerJS library, and connect you through my peer broker.

A window should pop up. It is draggable.

Click the File input box and select an image. It should be an exact pixel and color representation of what you want to implement within /r/place's pallete

The code diffs the loaded local image against the /r/place canvas and returns the different pixel location with its correct assignment to the slave

The slave executes the pixel placement by spoofing the POST request.

You will be ready to accept requests at this point.

## Slave

If you want to subscribe to a leader, open the peerjsslave.js file

Change the `var leaderPeerId = 'myChangableLeaderId';` at the top of the file to the unique leaderId I mentioned above (or to whoever you wish to subscribe)

Copy/paste the javascript into your developer console (F12) and hit enter.

This will load the PeerJS library, a peer connection will be brokered between you and the leader peer.

Upon connection, the leader peer diffs their locally loaded image against the /r/place canvas until a difference is found.

Once found, it will be reported back to your side and the instruction will be submitted as if you clicked that pixel.

You will need to refresh and wait the cool down timeout before doing another one. I hope in future updates to add leader peer management so cool downs are tracked and followup calls can be made after the cool down.
