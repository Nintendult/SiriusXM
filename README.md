# SiriusXM

*This fork has been modified to copy the AAC audio directly instead of converting to MP3,
allowing for no quality loss from what is broadcast. ID3 tags are not available.*

This script creates a server that serves HLSstreams for SiriusXM channels.
The recording mode can record shows from specific channels at source quality.

#### Requirements
Python libraries:
* eyeD3
* requests 
* tenacity

If you wish to record streams, you'll need to have [ffmpeg](https://www.ffmpeg.org/)
installed with [LAME](https://sourceforge.net/projects/lame/) support compiled in.

#### Installation
Install the Python dependencies

`pip install -r requirements.txt`


#### Configuration

You can store your XM credentials as environment variables if you don't want
to use the arg parser. Use `SIRIUSXM_USER` and `SIRIUSXM_PASS`.

```bash
export SIRIUSXM_USER="username"
export SIRIUSXM_PASS="password"
```

## Usage
#### Simple HLS server
`python sxm.py -u myuser -p mypassword`

Then in a player that supports HLS (QuickTime, VLC, ffmpeg, etc) you can
access a channel at http://127.0.0.1:8888/channel.m3u8 where "channel" is
the channel name, ID, or Sirius channel number.

#### Start the server in ripping mode
`python sxm.py -u myuser -p mypassword -c channel -r`

Shows are dumped locally using the short title
of the show which was recorded (i.e. `20180704180000-My_Program.mp3`)

Tagging occurs once the ffmpeg stream has been closed.


#### List all XM channels
`python sxm.py -u myuser -p mypassword -l`

Example output:

```bash
ID                  | Num | Name
big80s              | 8   | 80s on 8
90salternative      | 34  | Lithium
altnation           | 36  | Alt Nation
```
