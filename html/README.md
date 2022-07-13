# janus - vp9svctest 실행 방법

1. settings.js에서 server 주소를 기입합니다.
   1. ex) http://192.168.5.5:8088/janus // http는 8088, s는 8089
2. chrome 브라우저 실행 프로그램의 바로가기를 생성해서 다음과 같이 대상 옵션을 변경합니다.
   1. "C:\Program Files\Google\Chrome\Application\chrome.exe" --user-data-dir="C:\Users\reborn\.chromedata" --unsafely-treat-insecure-origin-as-secure="http://192.168.5.55:8080"
   2. 빈 폴더를 c드라이브 등에 생성해서 user-data-dir에 경로를 줍니다. 개발용 크롬 실행시 폴더 내부는 자동으로 초기화 됩니다.
   3. unsafely-treat-insecure-origin-as-secure는 live-server를 실행한 컴퓨터의 ipv4 주소와 실행된 포트번호를 기입합니다. 이유는 카메라 권한이 http로 실행 시 localhost로 한정되기 때문에 외부에서 192.168.5.55로 접속 시 카메라 권한이 거부되어 작동하지 않기 때문입니다.

## video room 연결 시 로그

Got a Janus API request from janus.transport.http (0x7f6850009240)
Creating new session: 1589377680997660; 0x7f689c0018e0
Session created (1589377680997660), create a queue for the long poll
Got a Janus API request from janus.transport.http (0x7f685000bd50)
Session 1589377680997660 found... returning up to 10 messages
Got a keep-alive on session 1589377680997660
Got a Janus API request from janus.transport.http (0x7f6850015500)
Creating new handle in session 1589377680997660: 8327038847505091; 0x7f689c0018e0 0x7f689c0020e0
[8327038847505091] Handle thread started; 0x7f689c0020e0

## 연결 해제 시 로그

Got a Janus API request from janus.transport.http (0x7f6850001c40)
Session is over and has not been claimed (5730129920046909), getting rid of the queue for the long poll
Destroying session 5730129920046909; 0x7f689c003800
[2807551449261721] Hanging up PeerConnection because of a Detach
Detaching handle from JANUS VideoRoom plugin; 0x7f689c0020e0 0x7f689c003280 0x7f689c0020e0 0x7f689c0032b0
[2807551449261721] Handle detached, scheduling destruction
[2807551449261721] Telling the plugin about the hangup (JANUS VideoRoom plugin)
[janus.plugin.videoroom-0x7f689c003280] No WebRTC media anymore; 0x7f689c0020e0 0x7f689c0032b0
[2807551449261721] Telling the plugin about the handle detach (JANUS VideoRoom plugin)
[2807551449261721] Sending event to transport...; 0x7f689c0020e0
[2807551449261721] Finalizing loop source
[2807551449261721] Handle thread ended! 0x7f689c0020e0
[2807551449261721] Handle and related resources freed; 0x7f689c0020e0 0x7f689c003800

## 재연결 시 로그

Got a Janus API request from janus.transport.http (0x7f685000c300)
Creating new session: 6603555770404060; 0x7f689c0018e0
Session created (6603555770404060), create a queue for the long poll
Got a Janus API request from janus.transport.http (0x7f6850002230)
Session 6603555770404060 found... returning up to 10 messages
Got a keep-alive on session 6603555770404060
Got a Janus API request from janus.transport.http (0x7f685000bd50)
Creating new handle in session 6603555770404060: 6187234239928544; 0x7f689c0018e0 0x7f689c0020e0
[6187234239928544] Handle thread started; 0x7f689c0020e0

## publish 버튼 클릭 시

Got a Janus API request from janus.transport.http (0x7f6850007610)
Transport task pool, serving request
[6187234239928544] There's a message for JANUS VideoRoom plugin
[6187234239928544] Remote SDP:
v=0
o=- 3384643649925114889 2 IN IP4 127.0.0.1
s=-
t=0 0
a=group:BUNDLE 0 1
a=extmap-allow-mixed
a=msid-semantic: WMS BHYZkO1x4dPnP053lJplz8DGdibY1JERkEV5
m=audio 9 UDP/TLS/RTP/SAVPF 111 63 103 104 9 0 8 106 105 13 110 112 113 126
c=IN IP4 0.0.0.0
a=rtcp:9 IN IP4 0.0.0.0
a=ice-ufrag:uqcp
a=ice-pwd:wUwmlGwnz6JT3JLjHHVRgs4B
a=ice-options:trickle
a=fingerprint:sha-256 AD:D3:94:14:0E:B3:1A:5E:09:22:D8:AD:B0:B5:37:DF:9A:F4:1C:D4:1A:5E:AC:CA:BE:BD:8C:29:64:21:BA:E1
a=setup:actpass
a=mid:0
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=sendonly
a=msid:BHYZkO1x4dPnP053lJplz8DGdibY1JERkEV5 dfd66c9b-5416-4e05-ab92-f905953bc1ac
a=rtcp-mux
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=fmtp:111 minptime=10;useinbandfec=1
a=rtpmap:63 red/48000/2
a=fmtp:63 111/111
a=rtpmap:103 ISAC/16000
a=rtpmap:104 ISAC/32000
a=rtpmap:9 G722/8000
a=rtpmap:0 PCMU/8000
a=rtpmap:8 PCMA/8000
a=rtpmap:106 CN/32000
a=rtpmap:105 CN/16000
a=rtpmap:13 CN/8000
a=rtpmap:110 telephone-event/48000
a=rtpmap:112 telephone-event/32000
a=rtpmap:113 telephone-event/16000
a=rtpmap:126 telephone-event/8000
a=ssrc:2649939362 cname:pRkWs0xYYaMl8Y/K
a=ssrc:2649939362 msid:BHYZkO1x4dPnP053lJplz8DGdibY1JERkEV5 dfd66c9b-5416-4e05-ab92-f905953bc1ac
m=video 9 UDP/TLS/RTP/SAVPF 96 97 98 99 100 101 127 121 125 107 108 109 124 120 123 119 35 36 41 42 114 115 116 117 118
c=IN IP4 0.0.0.0
a=rtcp:9 IN IP4 0.0.0.0
a=ice-ufrag:uqcp
a=ice-pwd:wUwmlGwnz6JT3JLjHHVRgs4B
a=ice-options:trickle
a=fingerprint:sha-256 AD:D3:94:14:0E:B3:1A:5E:09:22:D8:AD:B0:B5:37:DF:9A:F4:1C:D4:1A:5E:AC:CA:BE:BD:8C:29:64:21:BA:E1
a=setup:actpass
a=mid:1
a=extmap:14 urn:ietf:params:rtp-hdrext:toffset
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:13 urn:3gpp:video-orientation
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:5 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:6 http://www.webrtc.org/experiments/rtp-hdrext/video-content-type
a=extmap:7 http://www.webrtc.org/experiments/rtp-hdrext/video-timing
a=extmap:8 http://www.webrtc.org/experiments/rtp-hdrext/color-space
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=extmap:10 urn:ietf:params:rtp-hdrext:sdes:rtp-stream-id
a=extmap:11 urn:ietf:params:rtp-hdrext:sdes:repaired-rtp-stream-id
a=sendonly
a=msid:BHYZkO1x4dPnP053lJplz8DGdibY1JERkEV5 b7dbfa37-89d2-403c-9b18-0c053458939f
a=rtcp-mux
a=rtcp-rsize
a=rtpmap:96 VP8/90000
a=rtcp-fb:96 goog-remb
a=rtcp-fb:96 transport-cc
a=rtcp-fb:96 ccm fir
a=rtcp-fb:96 nack
a=rtcp-fb:96 nack pli
a=rtpmap:97 rtx/90000
a=fmtp:97 apt=96
a=rtpmap:98 VP9/90000
a=rtcp-fb:98 goog-remb
a=rtcp-fb:98 transport-cc
a=rtcp-fb:98 ccm fir
a=rtcp-fb:98 nack
a=rtcp-fb:98 nack pli
a=fmtp:98 profile-id=0
a=rtpmap:99 rtx/90000
a=fmtp:99 apt=98
a=rtpmap:100 VP9/90000
a=rtcp-fb:100 goog-remb
a=rtcp-fb:100 transport-cc
a=rtcp-fb:100 ccm fir
a=rtcp-fb:100 nack
a=rtcp-fb:100 nack pli
a=fmtp:100 profile-id=2
a=rtpmap:101 rtx/90000
a=fmtp:101 apt=100
a=rtpmap:127 H264/90000
a=rtcp-fb:127 goog-remb
a=rtcp-fb:127 transport-cc
a=rtcp-fb:127 ccm fir
a=rtcp-fb:127 nack
a=rtcp-fb:127 nack pli
a=fmtp:127 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=42001f
a=rtpmap:121 rtx/90000
a=fmtp:121 apt=127
a=rtpmap:125 H264/90000
a=rtcp-fb:125 goog-remb
a=rtcp-fb:125 transport-cc
a=rtcp-fb:125 ccm fir
a=rtcp-fb:125 nack
a=rtcp-fb:125 nack pli
a=fmtp:125 level-asymmetry-allowed=1;packetization-mode=0;profile-level-id=42001f
a=rtpmap:107 rtx/90000
a=fmtp:107 apt=125
a=rtpmap:108 H264/90000
a=rtcp-fb:108 goog-remb
a=rtcp-fb:108 transport-cc
a=rtcp-fb:108 ccm fir
a=rtcp-fb:108 nack
a=rtcp-fb:108 nack pli
a=fmtp:108 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=42e01f
a=rtpmap:109 rtx/90000
a=fmtp:109 apt=108
a=rtpmap:124 H264/90000
a=rtcp-fb:124 goog-remb
a=rtcp-fb:124 transport-cc
a=rtcp-fb:124 ccm fir
a=rtcp-fb:124 nack
a=rtcp-fb:124 nack pli
a=fmtp:124 level-asymmetry-allowed=1;packetization-mode=0;profile-level-id=42e01f
a=rtpmap:120 rtx/90000
a=fmtp:120 apt=124
a=rtpmap:123 H264/90000
a=rtcp-fb:123 goog-remb
a=rtcp-fb:123 transport-cc
a=rtcp-fb:123 ccm fir
a=rtcp-fb:123 nack
a=rtcp-fb:123 nack pli
a=fmtp:123 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=4d001f
a=rtpmap:119 rtx/90000
a=fmtp:119 apt=123
a=rtpmap:35 H264/90000
a=rtcp-fb:35 goog-remb
a=rtcp-fb:35 transport-cc
a=rtcp-fb:35 ccm fir
a=rtcp-fb:35 nack
a=rtcp-fb:35 nack pli
a=fmtp:35 level-asymmetry-allowed=1;packetization-mode=0;profile-level-id=4d001f
a=rtpmap:36 rtx/90000
a=fmtp:36 apt=35
a=rtpmap:41 AV1/90000
a=rtcp-fb:41 goog-remb
a=rtcp-fb:41 transport-cc
a=rtcp-fb:41 ccm fir
a=rtcp-fb:41 nack
a=rtcp-fb:41 nack pli
a=rtpmap:42 rtx/90000
a=fmtp:42 apt=41
a=rtpmap:114 H264/90000
a=rtcp-fb:114 goog-remb
a=rtcp-fb:114 transport-cc
a=rtcp-fb:114 ccm fir
a=rtcp-fb:114 nack
a=rtcp-fb:114 nack pli
a=fmtp:114 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=64001f
a=rtpmap:115 rtx/90000
a=fmtp:115 apt=114
a=rtpmap:116 red/90000
a=rtpmap:117 rtx/90000
a=fmtp:117 apt=116
a=rtpmap:118 ulpfec/90000
a=ssrc-group:FID 3965627334 1431248771
a=ssrc:3965627334 cname:pRkWs0xYYaMl8Y/K
a=ssrc:3965627334 msid:BHYZkO1x4dPnP053lJplz8DGdibY1JERkEV5 b7dbfa37-89d2-403c-9b18-0c053458939f
a=ssrc:1431248771 cname:pRkWs0xYYaMl8Y/K
a=ssrc:1431248771 msid:BHYZkO1x4dPnP053lJplz8DGdibY1JERkEV5 b7dbfa37-89d2-403c-9b18-0c053458939f
[6187234239928544] Peer advertised 'actpass' DTLS role, we'll be a DTLS client
[6187234239928544] There are 1 audio, 1 video and 0 data m-lines
[6187234239928544] Setting ICE locally: got OFFER
[6187234239928544] Creating ICE agent (ICE Full mode, controlled)
[6187234239928544] Adding 192.168.1.8 to the addresses to gather candidates for
[6187234239928544] Gathering done for stream 1
[6187234239928544] Parsing m-line #0...
[6187234239928544] ICE ufrag (local):   uqcp
[6187234239928544] ICE pwd (local):     wUwmlGwnz6JT3JLjHHVRgs4B
[6187234239928544] Fingerprint (local) : sha-256 AD:D3:94:14:0E:B3:1A:5E:09:22:D8:AD:B0:B5:37:DF:9A:F4:1C:D4:1A:5E:AC:CA:BE:BD:8C:29:64:21:BA:E1
[6187234239928544] DTLS setup (local):  actpass
[6187234239928544] Setting connect state (DTLS client)
[6187234239928544] Setting remote credentials...
[6187234239928544] Peer audio SSRC: 2649939362
[6187234239928544] Parsing m-line #1...
[6187234239928544] ICE ufrag (local):   uqcp
[6187234239928544] ICE pwd (local):     wUwmlGwnz6JT3JLjHHVRgs4B
[6187234239928544] Fingerprint (local) : sha-256 AD:D3:94:14:0E:B3:1A:5E:09:22:D8:AD:B0:B5:37:DF:9A:F4:1C:D4:1A:5E:AC:CA:BE:BD:8C:29:64:21:BA:E1
[6187234239928544] DTLS setup (local):  actpass
[6187234239928544] Setting connect state (DTLS client)
[6187234239928544] Peer video SSRC: 3965627334
[6187234239928544] Peer video SSRC (rtx): 1431248771
Got a Janus API request from janus.transport.http (0x7f6850004680)
[6187234239928544] Still processing the offer, queueing this trickle to wait until we're done there...
Will remove payload type 97 (97 rtx/90000)
Will remove payload type 99 (99 rtx/90000)
Will remove payload type 101 (101 rtx/90000)
Will remove payload type 121 (121 rtx/90000)
Will remove payload type 107 (107 rtx/90000)
Will remove payload type 109 (109 rtx/90000)
Will remove payload type 120 (120 rtx/90000)
Will remove payload type 119 (119 rtx/90000)
Will remove payload type 36 (36 rtx/90000)
Will remove payload type 42 (42 rtx/90000)
Will remove payload type 115 (115 rtx/90000)
Will remove payload type 116 (116 red/90000)
Will remove payload type 117 (117 rtx/90000)
Will remove payload type 118 (118 ulpfec/90000)
 -------------------------------------------
  >> Anonymized
 -------------------------------------------
Participant asked for video codec 'vp9' (room 5678, user 279039007438715)
Preparing JSON event as a reply
This is involving a negotiation (offer) as well:
v=0
o=- 3384643649925114889 2 IN IP4 1.1.1.1
s=-
t=0 0
m=audio 9 UDP/TLS/RTP/SAVPF 111 63 103 104 9 0 8 106 105 13 110 112 113 126
c=IN IP4 1.1.1.1
a=sendonly
a=mid:0
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=fmtp:111 minptime=10;useinbandfec=1
a=rtpmap:63 red/48000/2
a=fmtp:63 111/111
a=rtpmap:103 ISAC/16000
a=rtpmap:104 ISAC/32000
a=rtpmap:9 G722/8000
a=rtpmap:0 PCMU/8000
a=rtpmap:8 PCMA/8000
a=rtpmap:106 CN/32000
a=rtpmap:105 CN/16000
a=rtpmap:13 CN/8000
a=rtpmap:110 telephone-event/48000
a=rtpmap:112 telephone-event/32000
a=rtpmap:113 telephone-event/16000
a=rtpmap:126 telephone-event/8000
m=video 9 UDP/TLS/RTP/SAVPF 96 98 100 127 125 108 124 123 35 41 114
c=IN IP4 1.1.1.1
a=sendonly
a=mid:1
a=extmap:14 urn:ietf:params:rtp-hdrext:toffset
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:13 urn:3gpp:video-orientation
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:5 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:6 http://www.webrtc.org/experiments/rtp-hdrext/video-content-type
a=extmap:7 http://www.webrtc.org/experiments/rtp-hdrext/video-timing
a=extmap:8 http://www.webrtc.org/experiments/rtp-hdrext/color-space
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=extmap:10 urn:ietf:params:rtp-hdrext:sdes:rtp-stream-id
a=extmap:11 urn:ietf:params:rtp-hdrext:sdes:repaired-rtp-stream-id
a=rtpmap:96 VP8/90000
a=rtcp-fb:96 goog-remb
a=rtcp-fb:96 transport-cc
a=rtcp-fb:96 ccm fir
a=rtcp-fb:96 nack
a=rtcp-fb:96 nack pli
a=rtpmap:98 VP9/90000
a=rtcp-fb:98 goog-remb
a=rtcp-fb:98 transport-cc
a=rtcp-fb:98 ccm fir
a=rtcp-fb:98 nack
a=rtcp-fb:98 nack pli
a=fmtp:98 profile-id=0
a=rtpmap:100 VP9/90000
a=rtcp-fb:100 goog-remb
a=rtcp-fb:100 transport-cc
a=rtcp-fb:100 ccm fir
a=rtcp-fb:100 nack
a=rtcp-fb:100 nack pli
a=fmtp:100 profile-id=2
a=rtpmap:127 H264/90000
a=rtcp-fb:127 goog-remb
a=rtcp-fb:127 transport-cc
a=rtcp-fb:127 ccm fir
a=rtcp-fb:127 nack
a=rtcp-fb:127 nack pli
a=fmtp:127 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=42001f
a=rtpmap:125 H264/90000
a=rtcp-fb:125 goog-remb
a=rtcp-fb:125 transport-cc
a=rtcp-fb:125 ccm fir
a=rtcp-fb:125 nack
a=rtcp-fb:125 nack pli
a=fmtp:125 level-asymmetry-allowed=1;packetization-mode=0;profile-level-id=42001f
a=rtpmap:108 H264/90000
a=rtcp-fb:108 goog-remb
a=rtcp-fb:108 transport-cc
a=rtcp-fb:108 ccm fir
a=rtcp-fb:108 nack
a=rtcp-fb:108 nack pli
a=fmtp:108 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=42e01f
a=rtpmap:124 H264/90000
a=rtcp-fb:124 goog-remb
a=rtcp-fb:124 transport-cc
a=rtcp-fb:124 ccm fir
a=rtcp-fb:124 nack
a=rtcp-fb:124 nack pli
a=fmtp:124 level-asymmetry-allowed=1;packetization-mode=0;profile-level-id=42e01f
a=rtpmap:123 H264/90000
a=rtcp-fb:123 goog-remb
a=rtcp-fb:123 transport-cc
a=rtcp-fb:123 ccm fir
a=rtcp-fb:123 nack
a=rtcp-fb:123 nack pli
a=fmtp:123 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=4d001f
a=rtpmap:35 H264/90000
a=rtcp-fb:35 goog-remb
a=rtcp-fb:35 transport-cc
a=rtcp-fb:35 ccm fir
a=rtcp-fb:35 nack
a=rtcp-fb:35 nack pli
a=fmtp:35 level-asymmetry-allowed=1;packetization-mode=0;profile-level-id=4d001f
a=rtpmap:41 AV1/90000
a=rtcp-fb:41 goog-remb
a=rtcp-fb:41 transport-cc
a=rtcp-fb:41 ccm fir
a=rtcp-fb:41 nack
a=rtcp-fb:41 nack pli
a=rtpmap:114 H264/90000
a=rtcp-fb:114 goog-remb
a=rtcp-fb:114 transport-cc
a=rtcp-fb:114 ccm fir
a=rtcp-fb:114 nack
a=rtcp-fb:114 nack pli
a=fmtp:114 level-asymmetry-allowed=1;packetization-mode=1;profile-level-id=64001f

Handling publisher: turned this into an 'answer':
v=0
o=- 3384643649925114889 2 IN IP4 1.1.1.1
s=VideoRoom 5678
t=0 0
c=IN IP4 127.0.0.1
m=audio 9 UDP/TLS/RTP/SAVPF 111
c=IN IP4 127.0.0.1
a=recvonly
a=rtpmap:111 opus/48000/2
a=fmtp:111 useinbandfec=1
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
m=video 9 UDP/TLS/RTP/SAVPF 98
c=IN IP4 127.0.0.1
a=recvonly
a=rtpmap:98 VP9/90000
a=rtcp-fb:98 ccm fir
a=rtcp-fb:98 nack
a=rtcp-fb:98 nack pli
a=rtcp-fb:98 goog-remb
a=rtcp-fb:98 transport-cc
a=extmap:13 urn:3gpp:video-orientation
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:5 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=extmap:10 urn:ietf:params:rtp-hdrext:sdes:rtp-stream-id
a=extmap:11 urn:ietf:params:rtp-hdrext:sdes:repaired-rtp-stream-id
a=fmtp:98 profile-id=0

[6187234239928544] There are 1 audio, 1 video and 0 data m-lines
 -------------------------------------------
  >> Anonymized
 -------------------------------------------
[6187234239928544] We have 1 candidates for Stream #1, Component #1
[6187234239928544]   Address:    192.168.1.8:35801
[6187234239928544]   Priority:   2013266431
[6187234239928544]   Foundation: 1
[6187234239928544]     1 1 udp 2013266431 192.168.1.8 35801 typ host
[6187234239928544] We have 1 candidates for Stream #1, Component #1
[6187234239928544]   Address:    192.168.1.8:35801
[6187234239928544]   Priority:   2013266431
[6187234239928544]   Foundation: 1
[6187234239928544]     1 1 udp 2013266431 192.168.1.8 35801 typ host
 -------------------------------------------
  >> Merged (1676 bytes)
 -------------------------------------------
v=0
o=- 3384643649925114889 2 IN IP4 192.168.1.8
s=VideoRoom 5678
t=0 0
a=group:BUNDLE 0 1
a=ice-options:trickle
a=fingerprint:sha-256 23:3C:E6:E0:F0:68:19:C3:AA:F8:ED:8C:22:99:13:AA:83:AF:C7:76:38:67:B6:20:03:1C:2D:E7:D8:57:C0:40
a=extmap-allow-mixed
a=msid-semantic: WMS janus
m=audio 9 UDP/TLS/RTP/SAVPF 111
c=IN IP4 192.168.1.8
a=recvonly
a=mid:0
a=rtcp-mux
a=ice-ufrag:GEHH
a=ice-pwd:GwkILOAezVNjXYYyEdMvuB
a=ice-options:trickle
a=setup:active
a=rtpmap:111 opus/48000/2
a=fmtp:111 useinbandfec=1
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=msid:janus janus0
a=ssrc:3025530726 cname:janus
a=candidate:1 1 udp 2013266431 192.168.1.8 35801 typ host
a=end-of-candidates
m=video 9 UDP/TLS/RTP/SAVPF 98 99
c=IN IP4 192.168.1.8
a=recvonly
a=mid:1
a=rtcp-mux
a=ice-ufrag:GEHH
a=ice-pwd:GwkILOAezVNjXYYyEdMvuB
a=ice-options:trickle
a=setup:active
a=rtpmap:98 VP9/90000
a=rtcp-fb:98 ccm fir
a=rtcp-fb:98 nack
a=rtcp-fb:98 nack pli
a=rtcp-fb:98 goog-remb
a=rtcp-fb:98 transport-cc
a=extmap:13 urn:3gpp:video-orientation
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:5 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=extmap:10 urn:ietf:params:rtp-hdrext:sdes:rtp-stream-id
a=extmap:11 urn:ietf:params:rtp-hdrext:sdes:repaired-rtp-stream-id
a=fmtp:98 profile-id=0
a=rtpmap:99 rtx/90000
a=fmtp:99 apt=98
a=msid:janus janus1
a=ssrc:2652415751 cname:janus
a=ssrc:1071558425 cname:janus
a=candidate:1 1 udp 2013266431 192.168.1.8 35801 typ host
a=end-of-candidates

[6187234239928544] Sending answer, ready to setup remote candidates and send connectivity checks...
[6187234239928544]   -- Processing 1 pending trickle candidates
[6187234239928544] Trickle candidate (0): candidate:2894319779 1 udp 2122260223 192.168.1.52 57473 typ host generation 0 ufrag uqcp network-id 1
[6187234239928544]  Adding remote candidate component:1 stream:1 type:host 192.168.1.52:57473
[6187234239928544]  Transport: UDP
[6187234239928544] SDP processed but ICE not started yet for this component, setting candidates we have up to now
[6187234239928544] ## Setting remote candidates: stream 1, component 1 (1 in the list)
[6187234239928544] Queueing candidate 0x7f6870007220 (startup)
[6187234239928544] Done! Sending connectivity checks...
[6187234239928544] Component 1 in stream 1 has already been set up
[6187234239928544] Sending event to transport...
[6187234239928544] Processing candidate 0x7f6870007220
  >> Pushing event: 0 (took 375 us)
[6187234239928544] Component state changed for component 1 in stream 1: 2 (connecting)
[6187234239928544] 1 remote candidate added
Got a Janus API request from janus.transport.http (0x7f68500013d0)
[6187234239928544] Trickle candidate (1): candidate:2894319779 1 udp 2122260223 192.168.1.52 57474 typ host generation 0 ufrag uqcp network-id 1
[6187234239928544] Got a mid='1' candidate (index 1) but we're bundling, ignoring...
Got a Janus API request from janus.transport.http (0x7f6850004680)
Session 6603555770404060 found... returning up to 10 messages
Got a keep-alive on session 6603555770404060
Got a Janus API request from janus.transport.http (0x7f6850008520)
No more remote candidates for handle 6187234239928544!
[6187234239928544] New selected pair for component 1 in stream 1: 1 <-> 2894319779
[6187234239928544]   Component is ready enough, starting DTLS handshake...
[6187234239928544] Component state changed for component 1 in stream 1: 3 (connected)
[6187234239928544] Component state changed for component 1 in stream 1: 4 (ready)
[6187234239928544] Creating retransmission timer with ID 41
[6187234239928544] DTLS established, yay!
[6187234239928544] Computing sha-256 fingerprint of remote certificate...
[6187234239928544] Remote fingerprint (sha-256) of the client is AD:D3:94:14:0E:B3:1A:5E:09:22:D8:AD:B0:B5:37:DF:9A:F4:1C:D4:1A:5E:AC:CA:BE:BD:8C:29:64:21:BA:E1
[6187234239928544]  Fingerprint is a match!
[6187234239928544] SRTP_AES128_CM_SHA1_80
[6187234239928544] Key/Salt/Master: 30/16/14
[6187234239928544] Created inbound SRTP session for component 1 in stream 1
[6187234239928544] Created outbound SRTP session for component 1 in stream 1
[6187234239928544] The DTLS handshake for the component 1 in stream 1 has been completed
[6187234239928544] The DTLS handshake has been completed
[6187234239928544] Telling the plugin about it (JANUS VideoRoom plugin)
[janus.plugin.videoroom-0x7f685000be90] WebRTC media is now available
Notifying participant 5666006655618166 (qwe)
[8559947248405975] Sending event to transport...
  >> 0 (Success)
[6187234239928544] Sending event to transport...; 0x7f689c0020e0
Got a Janus API request from janus.transport.http (0x7f6850004680)
Creating new handle in session 3643103484027879: 2258175459935508; 0x7f6850001f20 0x7f689c007c30
[2258175459935508] Handle thread started; 0x7f689c007c30
Got a Janus API request from janus.transport.http (0x7f68500013d0)
Session 3643103484027879 found... returning up to 10 messages
Got a keep-alive on session 3643103484027879
Got a Janus API request from janus.transport.http (0x7f68500069c0)
Session 6603555770404060 found... returning up to 10 messages
Got a keep-alive on session 6603555770404060
SSRC changed, 0 --> 2649939362
[6187234239928544] Notifying that we are receiving audio on mid 0
[6187234239928544] Sending event to transport...
Got a Janus API request from janus.transport.http (0x7f68500069c0)
Transport task pool, serving request
[2258175459935508] There's a message for JANUS VideoRoom plugin
Configuring new participant
Configuring new subscriber
Preparing JSON event as a reply
[2258175459935508] There are 1 audio, 1 video and 0 data m-lines
[2258175459935508] Setting ICE locally: got ANSWER
[2258175459935508] Creating ICE agent (ICE Full mode, controlling)
[2258175459935508] Adding 192.168.1.8 to the addresses to gather candidates for
[2258175459935508] Gathering done for stream 1
 -------------------------------------------
  >> Anonymized
 -------------------------------------------
[2258175459935508] We have 1 candidates for Stream #1, Component #1
[2258175459935508]   Address:    192.168.1.8:39998
[2258175459935508]   Priority:   2013266431
[2258175459935508]   Foundation: 1
[2258175459935508]     1 1 udp 2013266431 192.168.1.8 39998 typ host
[2258175459935508] We have 1 candidates for Stream #1, Component #1
[2258175459935508]   Address:    192.168.1.8:39998
[2258175459935508]   Priority:   2013266431
[2258175459935508]   Foundation: 1
[2258175459935508]     1 1 udp 2013266431 192.168.1.8 39998 typ host
 -------------------------------------------
  >> Merged (1699 bytes)
 -------------------------------------------
v=0
o=- 1657699801430735 1 IN IP4 192.168.1.8
s=VideoRoom 5678
t=0 0
a=group:BUNDLE 0 1
a=ice-options:trickle
a=fingerprint:sha-256 23:3C:E6:E0:F0:68:19:C3:AA:F8:ED:8C:22:99:13:AA:83:AF:C7:76:38:67:B6:20:03:1C:2D:E7:D8:57:C0:40
a=extmap-allow-mixed
a=msid-semantic: WMS janus
m=audio 9 UDP/TLS/RTP/SAVPF 111
c=IN IP4 192.168.1.8
a=sendonly
a=mid:0
a=rtcp-mux
a=ice-ufrag:ZoA3
a=ice-pwd:p+I2HHKbKPqHa4zgCrMqps
a=ice-options:trickle
a=setup:actpass
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=fmtp:111 useinbandfec=1
a=msid:janus janus0
a=ssrc:786487451 cname:janus
a=candidate:1 1 udp 2013266431 192.168.1.8 39998 typ host
a=end-of-candidates
m=video 9 UDP/TLS/RTP/SAVPF 101 102
c=IN IP4 192.168.1.8
a=sendonly
a=mid:1
a=rtcp-mux
a=ice-ufrag:ZoA3
a=ice-pwd:p+I2HHKbKPqHa4zgCrMqps
a=ice-options:trickle
a=setup:actpass
a=rtpmap:101 VP9/90000
a=rtcp-fb:101 ccm fir
a=rtcp-fb:101 nack
a=rtcp-fb:101 nack pli
a=rtcp-fb:101 goog-remb
a=rtcp-fb:101 transport-cc
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=extmap:12 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:13 urn:3gpp:video-orientation
a=fmtp:101 profile-id=0
a=rtpmap:102 rtx/90000
a=fmtp:102 apt=101
a=ssrc-group:FID 2674116580 1561370748
a=msid:janus janus1
a=ssrc:2674116580 cname:janus
a=ssrc:1561370748 cname:janus
a=candidate:1 1 udp 2013266431 192.168.1.8 39998 typ host
a=end-of-candidates

[2258175459935508] Sending event to transport...
  >> Pushing event: 0 (took 1055 us)
Got a Janus API request from janus.transport.http (0x7f68500013d0)
Session 6603555770404060 found... returning up to 10 messages
Got a keep-alive on session 6603555770404060
Got a Janus API request from janus.transport.http (0x7f6850004680)
Session 3643103484027879 found... returning up to 10 messages
Got a keep-alive on session 3643103484027879
Got a Janus API request from janus.transport.http (0x7f6850004b80)
Transport task pool, serving request
[2258175459935508] There's a message for JANUS VideoRoom plugin
[2258175459935508] Remote SDP:
v=0
o=- 7332148811067671817 2 IN IP4 127.0.0.1
s=-
t=0 0
a=group:BUNDLE 0 1
a=extmap-allow-mixed
a=msid-semantic: WMS
m=audio 9 UDP/TLS/RTP/SAVPF 111
c=IN IP4 0.0.0.0
a=rtcp:9 IN IP4 0.0.0.0
a=ice-ufrag:mVF7
a=ice-pwd:sdtN1i4JM3bzstpf6J+zWGxp
a=ice-options:trickle
a=fingerprint:sha-256 C0:57:5E:06:16:1F:97:0D:0F:40:9F:30:5C:71:D0:F6:32:56:6A:F8:A1:70:97:A4:53:89:1C:59:35:0C:07:62
a=setup:active
a=mid:0
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=recvonly
a=rtcp-mux
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=fmtp:111 minptime=10;useinbandfec=1
m=video 9 UDP/TLS/RTP/SAVPF 101 102
c=IN IP4 0.0.0.0
a=rtcp:9 IN IP4 0.0.0.0
a=ice-ufrag:mVF7
a=ice-pwd:sdtN1i4JM3bzstpf6J+zWGxp
a=ice-options:trickle
a=fingerprint:sha-256 C0:57:5E:06:16:1F:97:0D:0F:40:9F:30:5C:71:D0:F6:32:56:6A:F8:A1:70:97:A4:53:89:1C:59:35:0C:07:62
a=setup:active
a=mid:1
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:13 urn:3gpp:video-orientation
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:12 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=recvonly
a=rtcp-mux
a=rtpmap:101 VP9/90000
a=rtcp-fb:101 goog-remb
a=rtcp-fb:101 transport-cc
a=rtcp-fb:101 ccm fir
a=rtcp-fb:101 nack
a=rtcp-fb:101 nack pli
a=fmtp:101 profile-id=0
a=rtpmap:102 rtx/90000
a=fmtp:102 apt=101
[2258175459935508] There are 1 audio, 1 video and 0 data m-lines
[2258175459935508] Parsing m-line #0...
[2258175459935508] ICE ufrag (local):   mVF7
[2258175459935508] ICE pwd (local):     sdtN1i4JM3bzstpf6J+zWGxp
[2258175459935508] Fingerprint (local) : sha-256 C0:57:5E:06:16:1F:97:0D:0F:40:9F:30:5C:71:D0:F6:32:56:6A:F8:A1:70:97:A4:53:89:1C:59:35:0C:07:62
[2258175459935508] DTLS setup (local):  active
[2258175459935508] Setting accept state (DTLS server)
[2258175459935508] Setting remote credentials...
[2258175459935508] Parsing m-line #1...
[2258175459935508] ICE ufrag (local):   mVF7
[2258175459935508] ICE pwd (local):     sdtN1i4JM3bzstpf6J+zWGxp
[2258175459935508] Fingerprint (local) : sha-256 C0:57:5E:06:16:1F:97:0D:0F:40:9F:30:5C:71:D0:F6:32:56:6A:F8:A1:70:97:A4:53:89:1C:59:35:0C:07:62
[2258175459935508] DTLS setup (local):  active
[2258175459935508] Setting accept state (DTLS server)
[2258175459935508]   -- ICE Trickling is supported by the browser, waiting for remote candidates...
Will remove payload type 102 (102 rtx/90000)
 -------------------------------------------
  >> Anonymized
 -------------------------------------------
Preparing JSON event as a reply
This is involving a negotiation (answer) as well:
v=0
o=- 7332148811067671817 2 IN IP4 1.1.1.1
s=-
t=0 0
m=audio 9 UDP/TLS/RTP/SAVPF 111
c=IN IP4 1.1.1.1
a=recvonly
a=mid:0
a=extmap:1 urn:ietf:params:rtp-hdrext:ssrc-audio-level
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=fmtp:111 minptime=10;useinbandfec=1
m=video 9 UDP/TLS/RTP/SAVPF 101
c=IN IP4 1.1.1.1
a=recvonly
a=mid:1
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:13 urn:3gpp:video-orientation
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:12 http://www.webrtc.org/experiments/rtp-hdrext/playout-delay
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=rtpmap:101 VP9/90000
a=rtcp-fb:101 goog-remb
a=rtcp-fb:101 transport-cc
a=rtcp-fb:101 ccm fir
a=rtcp-fb:101 nack
a=rtcp-fb:101 nack pli
a=fmtp:101 profile-id=0

[2258175459935508] Sending event to transport...
  >> 0 (Success)
[6187234239928544] DTLS already set up, disabling retransmission timer!
[2258175459935508] Discovered new remote candidate for component 1 in stream 1: type=prflx
[2258175459935508] Stream #1, Component #1
[2258175459935508]   Address:    192.168.1.52:49327
[2258175459935508]   Priority:   1853824767
[2258175459935508]   Foundation: remote1
[2258175459935508]  Adding remote candidate component:1 stream:1 type:prflx 192.168.1.52:49327 --> 192.168.1.52:49327
[2258175459935508]  Transport: UDP
[2258175459935508] ICE already started for this component, setting candidates we have up to now
[2258175459935508] ## Setting remote candidates: stream 1, component 1 (1 in the list)
[2258175459935508] Queueing candidate 0x7f689c008190 (startup)
[2258175459935508] Component state changed for component 1 in stream 1: 2 (connecting)
[2258175459935508] Processing candidate 0x7f689c008190
[2258175459935508] 1 remote candidate added
Got a Janus API request from janus.transport.http (0x7f6850004680)
[2258175459935508] Trickle candidate (0): candidate:2894319779 1 udp 2122260223 192.168.1.52 49327 typ host generation 0 ufrag mVF7 network-id 1
[2258175459935508]  Adding remote candidate component:1 stream:1 type:host 192.168.1.52:49327
[2258175459935508]  Transport: UDP
[2258175459935508] Queueing candidate 0x7f6840013360
[2258175459935508] Processing candidate 0x7f6840013360
[2258175459935508] 1 remote candidate added
Got a Janus API request from janus.transport.http (0x7f68500055c0)
Session 3643103484027879 found... returning up to 10 messages
Got a keep-alive on session 3643103484027879
Got a Janus API request from janus.transport.http (0x7f68500026e0)
No more remote candidates for handle 2258175459935508!
[2258175459935508] New selected pair for component 1 in stream 1: 1 <-> 2894319779
[2258175459935508]   Component is ready enough, starting DTLS handshake...
[2258175459935508] Component state changed for component 1 in stream 1: 3 (connected)
[2258175459935508] Component state changed for component 1 in stream 1: 4 (ready)
[2258175459935508] Creating retransmission timer with ID 5
[2258175459935508] DTLS established, yay!
[2258175459935508] Computing sha-256 fingerprint of remote certificate...
[2258175459935508] Remote fingerprint (sha-256) of the client is C0:57:5E:06:16:1F:97:0D:0F:40:9F:30:5C:71:D0:F6:32:56:6A:F8:A1:70:97:A4:53:89:1C:59:35:0C:07:62
[2258175459935508]  Fingerprint is a match!
[2258175459935508] SRTP_AEAD_AES_256_GCM
[2258175459935508] Key/Salt/Master: 44/32/12
[2258175459935508] Created inbound SRTP session for component 1 in stream 1
[2258175459935508] Created outbound SRTP session for component 1 in stream 1
[2258175459935508] The DTLS handshake for the component 1 in stream 1 has been completed
[2258175459935508] The DTLS handshake has been completed
[2258175459935508] Telling the plugin about it (JANUS VideoRoom plugin)
[janus.plugin.videoroom-0x7f685000af60] WebRTC media is now available
New subscriber available sending PLI to 279039007438715 (#1, test)
[2258175459935508] Sending event to transport...; 0x7f689c007c30
[2258175459935508] DTLS already set up, disabling retransmission timer!
SSRC changed, 0 --> 2649939362
Got a Janus API request from janus.transport.http (0x7f68500055c0)
Session 3643103484027879 found... returning up to 10 messages
Got a keep-alive on session 3643103484027879
SSRC changed, 0 --> 3965627334
SSRC changed, 0 --> 3965627334
Sending REMB (test, 512000)
[6187234239928544] Notifying that we are receiving video on mid 1
[6187234239928544] Sending event to transport...

## unpublish 클릭 시 로그

Got a Janus API request from janus.transport.http (0x7f6850001f20)
Transport task pool, serving request
[7342526508459416] There's a message for JANUS VideoRoom plugin
[janus.plugin.videoroom-0x7f689c005990] No WebRTC media anymore; 0x7f689c0020e0 0x7f689c0018e0
[1019465128787416] There are 1 audio, 1 video and 0 data m-lines
[1019465128787416] Updating existing session
 -------------------------------------------
  >> Anonymized
 -------------------------------------------
[1019465128787416] We have 1 candidates for Stream #1, Component #1
[1019465128787416]   Address:    192.168.1.8:57725
[1019465128787416]   Priority:   2013266431
[1019465128787416]   Foundation: 1
[1019465128787416]     1 1 udp 2013266431 192.168.1.8 57725 typ host
[1019465128787416] We have 1 candidates for Stream #1, Component #1
[1019465128787416]   Address:    192.168.1.8:57725
[1019465128787416]   Priority:   2013266431
[1019465128787416]   Foundation: 1
[1019465128787416]     1 1 udp 2013266431 192.168.1.8 57725 typ host
 -------------------------------------------
  >> Merged (1372 bytes)
 -------------------------------------------
v=0
o=- 1657699888638820 2 IN IP4 192.168.1.8
s=VideoRoom 5678
t=0 0
a=group:BUNDLE 0 1
a=ice-options:trickle
a=fingerprint:sha-256 23:3C:E6:E0:F0:68:19:C3:AA:F8:ED:8C:22:99:13:AA:83:AF:C7:76:38:67:B6:20:03:1C:2D:E7:D8:57:C0:40
a=extmap-allow-mixed
a=msid-semantic: WMS janus
m=audio 9 UDP/TLS/RTP/SAVPF 111
c=IN IP4 192.168.1.8
a=inactive
a=mid:0
a=rtcp-mux
a=ice-ufrag:x16d
a=ice-pwd:RAELu9vwQcHu6yRXBxfxZI
a=ice-options:trickle
a=setup:actpass
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=msid:janus janus0
a=candidate:1 1 udp 2013266431 192.168.1.8 57725 typ host
a=end-of-candidates
m=video 9 UDP/TLS/RTP/SAVPF 101 102
c=IN IP4 192.168.1.8
a=inactive
a=mid:1
a=rtcp-mux
a=ice-ufrag:x16d
a=ice-pwd:RAELu9vwQcHu6yRXBxfxZI
a=ice-options:trickle
a=setup:actpass
a=rtpmap:101 VP9/90000
a=rtcp-fb:101 ccm fir
a=rtcp-fb:101 nack
a=rtcp-fb:101 nack pli
a=rtcp-fb:101 goog-remb
a=rtcp-fb:101 transport-cc
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=fmtp:101 profile-id=0
a=rtpmap:102 rtx/90000
a=fmtp:102 apt=101
a=msid:janus janus1
a=candidate:1 1 udp 2013266431 192.168.1.8 57725 typ host
a=end-of-candidates

[1019465128787416] Sending event to transport...
  >> Pushing event: 0 (took 415 us)
Notifying participant 5828802084310127 (qwe)
[7633668388113572] Sending event to transport...
  >> 0 (Success)
Preparing JSON event as a reply
[7342526508459416] Sending event to transport...
  >> 0 (Success)
Got a Janus API request from janus.transport.http (0x7f6850007d00)
Session 4960491800350756 found... returning up to 10 messages
Got a keep-alive on session 4960491800350756
Got a Janus API request from janus.transport.http (0x7f6850007d00)
Session 5833571753191105 found... returning up to 10 messages
Got a keep-alive on session 5833571753191105
[7342526508459416] Got RTCP BYE on stream 1 (component 1)
Got a Janus API request from janus.transport.http (0x7f6850015540)
Transport task pool, serving request
[1019465128787416] There's a message for JANUS VideoRoom plugin
[1019465128787416] Remote SDP:
v=0
o=- 5741195042511203179 3 IN IP4 127.0.0.1
s=-
t=0 0
a=group:BUNDLE 0 1
a=extmap-allow-mixed
a=msid-semantic: WMS
m=audio 57135 UDP/TLS/RTP/SAVPF 111
c=IN IP4 192.168.1.52
a=rtcp:9 IN IP4 0.0.0.0
a=candidate:2894319779 1 udp 2122260223 192.168.1.52 57135 typ host generation 0 network-id 1
a=ice-ufrag:SWDp
a=ice-pwd:w0CfWFNvr6aXaO0KIX8m8Yu5
a=ice-options:trickle
a=fingerprint:sha-256 68:C3:68:B1:EE:74:B9:7E:7B:0E:49:31:6A:21:6F:91:AF:77:E4:35:B6:2C:E9:7F:E5:A1:BE:9B:52:7B:F0:73
a=setup:active
a=mid:0
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=inactive
a=rtcp-mux
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=fmtp:111 minptime=10;useinbandfec=1
m=video 9 UDP/TLS/RTP/SAVPF 101 102
c=IN IP4 0.0.0.0
a=rtcp:9 IN IP4 0.0.0.0
a=ice-ufrag:SWDp
a=ice-pwd:w0CfWFNvr6aXaO0KIX8m8Yu5
a=ice-options:trickle
a=fingerprint:sha-256 68:C3:68:B1:EE:74:B9:7E:7B:0E:49:31:6A:21:6F:91:AF:77:E4:35:B6:2C:E9:7F:E5:A1:BE:9B:52:7B:F0:73
a=setup:active
a=mid:1
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=inactive
a=rtcp-mux
a=rtpmap:101 VP9/90000
a=rtcp-fb:101 goog-remb
a=rtcp-fb:101 transport-cc
a=rtcp-fb:101 ccm fir
a=rtcp-fb:101 nack
a=rtcp-fb:101 nack pli
a=fmtp:101 profile-id=0
a=rtpmap:102 rtx/90000
a=fmtp:102 apt=101
[1019465128787416] There are 1 audio, 1 video and 0 data m-lines
[1019465128787416] Negotiation update, checking what changed...
[1019465128787416] Parsing m-line #0...
[1019465128787416] ICE ufrag (local):   SWDp
[1019465128787416] ICE pwd (local):     w0CfWFNvr6aXaO0KIX8m8Yu5
[1019465128787416] Fingerprint (local) : sha-256 68:C3:68:B1:EE:74:B9:7E:7B:0E:49:31:6A:21:6F:91:AF:77:E4:35:B6:2C:E9:7F:E5:A1:BE:9B:52:7B:F0:73
[1019465128787416] DTLS setup (local):  active
[1019465128787416]  Adding remote candidate component:1 stream:1 type:host 192.168.1.52:57135
[1019465128787416]  Transport: UDP
[1019465128787416] Parsing m-line #1...
[1019465128787416] ICE ufrag (local):   SWDp
[1019465128787416] ICE pwd (local):     w0CfWFNvr6aXaO0KIX8m8Yu5
[1019465128787416] Fingerprint (local) : sha-256 68:C3:68:B1:EE:74:B9:7E:7B:0E:49:31:6A:21:6F:91:AF:77:E4:35:B6:2C:E9:7F:E5:A1:BE:9B:52:7B:F0:73
[1019465128787416] DTLS setup (local):  active
Will remove payload type 102 (102 rtx/90000)
 -------------------------------------------
  >> Anonymized
 -------------------------------------------
Preparing JSON event as a reply
This is involving a negotiation (answer) as well:
v=0
o=- 5741195042511203179 3 IN IP4 1.1.1.1
s=-
t=0 0
m=audio 9 UDP/TLS/RTP/SAVPF 111
c=IN IP4 1.1.1.1
a=inactive
a=mid:0
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=rtpmap:111 opus/48000/2
a=rtcp-fb:111 transport-cc
a=fmtp:111 minptime=10;useinbandfec=1
m=video 9 UDP/TLS/RTP/SAVPF 101
c=IN IP4 1.1.1.1
a=inactive
a=mid:1
a=extmap:2 http://www.webrtc.org/experiments/rtp-hdrext/abs-send-time
a=extmap:3 http://www.ietf.org/id/draft-holmer-rmcat-transport-wide-cc-extensions-01
a=extmap:4 urn:ietf:params:rtp-hdrext:sdes:mid
a=rtpmap:101 VP9/90000
a=rtcp-fb:101 goog-remb
a=rtcp-fb:101 transport-cc
a=rtcp-fb:101 ccm fir
a=rtcp-fb:101 nack
a=rtcp-fb:101 nack pli
a=fmtp:101 profile-id=0

  -- Updating existing publisher
[1019465128787416] Sending event to transport...
  >> 0 (Success)
[1019465128787416] DTLS alert triggered on stream 1 (component 1), closing...
[1019465128787416] Hanging up PeerConnection because of a DTLS alert
[1019465128787416] DTLS alert triggered on stream 1 (component 1), closing...
[1019465128787416] Telling the plugin about the hangup (JANUS VideoRoom plugin)
[janus.plugin.videoroom-0x7f689c0054f0] No WebRTC media anymore; 0x7f689c007d40 0x7f689c0077a0
[1019465128787416] Removing stream 1 from agent 0x7f6840014540
[1019465128787416] Closing nice agent 0x7f6840014540
[1019465128787416] Notifying WebRTC hangup; 0x7f689c007d40
[1019465128787416] Sending event to transport...; 0x7f689c007d40
[1019465128787416] WebRTC resources freed; 0x7f689c007d40 0x7f689c005da0
[1019465128787416] Disposing nice agent 0x7f6840014540
[7342526508459416] DTLS alert triggered on stream 1 (component 1), closing...
[7342526508459416] Hanging up PeerConnection because of a DTLS alert
[7342526508459416] DTLS alert triggered on stream 1 (component 1), closing...
[7342526508459416] Telling the plugin about the hangup (JANUS VideoRoom plugin)
[janus.plugin.videoroom-0x7f689c005990] No WebRTC media anymore; 0x7f689c0020e0 0x7f689c0018e0
Notifying participant 5828802084310127 (qwe)
[7633668388113572] Sending event to transport...
  >> 0 (Success)
[7342526508459416] Removing stream 1 from agent 0x7f6870018930
[7342526508459416] Closing nice agent 0x7f6870018930
[7342526508459416] Notifying WebRTC hangup; 0x7f689c0020e0
[7342526508459416] Sending event to transport...; 0x7f689c0020e0
[7342526508459416] WebRTC resources freed; 0x7f689c0020e0 0x7f6850004600
[7342526508459416] Disposing nice agent 0x7f6870018930
Got a Janus API request from janus.transport.http (0x7f6850007d00)
Session 4960491800350756 found... returning up to 10 messages
Got a keep-alive on session 4960491800350756
Got a Janus API request from janus.transport.http (0x7f6850007d00)
Detaching handle from JANUS VideoRoom plugin; 0x7f689c007d40 0x7f689c0054f0 0x7f689c007d40 0x7f689c0077a0
[1019465128787416] Handle detached, scheduling destruction
[1019465128787416] Telling the plugin about the handle detach (JANUS VideoRoom plugin)
[1019465128787416] Sending event to transport...; 0x7f689c007d40
[1019465128787416] Finalizing loop source
[1019465128787416] Handle thread ended! 0x7f689c007d40
[1019465128787416] Handle and related resources freed; 0x7f689c007d40 0x7f689c005da0

## 야누스 서버와 주기적 통신 keepalive 로그

Got a Janus API request from janus.transport.http (0x7f6850007d40)
Session 5736093198365670 found... returning up to 10 messages
Got a keep-alive on session 5736093198365670

## local video bandwidth 변경 시 로그

Got a Janus API request from janus.transport.http (0x7f68500088a0)
Transport task pool, serving request
[2707550221049444] There's a message for JANUS VideoRoom plugin
Setting video bitrate: 1500000 (room 5678, user 2602131993088735)
Preparing JSON event as a reply
[2707550221049444] Sending event to transport...
  >> 0 (Success)
Got a Janus API request from janus.transport.http (0x7f6850007d80)
Session 5736093198365670 found... returning up to 10 messages
Got a keep-alive on session 5736093198365670
Regular keyframe request sending PLI to 2602131993088735 (#1, qwe)
