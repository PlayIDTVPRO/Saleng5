
<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="OpenPlayerJS is an ever-green lightweight media player that supports the most common video/audio files for the web, and also VAST/VPAID/VMAP Ads">
    <meta name="google-site-verification" content="Desj0WKx8CJ5bVxUndGN6WP9k80dxk7fZg0ChsKmIno" />
    <title>Player JS PlayIDTV</title>

    <link rel="shortcut icon" href="img/favicon.png" type="image/x-icon">
    <link rel="icon" href="img/favicon.png" type="image/x-icon">
    <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/openplayerjs@latest/dist/openplayer.min.css">
</head>

<body>
    <div id="media"></div>
    <script src="js/iframeResizer.contentWindow.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/openplayerjs@latest/dist/openplayer.min.js"></script>
    <script>
        if(window.top === window.self) {
            document.body.style.background = '#000';
            document.body.style.color = '#fff';
            document.body.style.height = '100%';
            document.body.style.margin = 0;
            document.body.style.overflow = 'hidden';
            document.body.style.padding = 0;
            document.body.style.position = 'absolute';
            document.body.style.width = '100%';

            var media = document.getElementById('media');
            media.style.left = '50%';
            media.style.position = 'absolute';
            media.style.top = '50%';
            media.style.transform = 'translate(-50%, -50%)';
            media.style.width = '100%';
        }
        function getUrlParameter(name) {
            name = name.replace(/[\[]/, '\\[').replace(/[\]]/, '\\]');
            var regex = new RegExp('[\\?&]' + name + '=([^&#]*)');
            var results = regex.exec(location.search);
            return results === null ? '' : decodeURIComponent(results[1].replace(/\+/g, ' '));
        };
        var type = getUrlParameter('type');
        function getMimeType(url) {
            if (/\.m3u8/i.test(url)) {
                return 'application/x-mpegURL';
            } else if (/\.mpd/i.test(url)) {
                return 'application/dash+xml';
            } else if (/\.mp4/i.test(url)) {
                return type === 'audio' ? 'audio/mp4' : 'video/mp4';
            } else if (/\.mp3/i.test(url)) {
                return 'audio/mp3';
            } else if (/\.webm/i.test(url)) {
                return type === 'audio' ? 'audio/webm' : 'video/webm';
            } else if (/\.ogg/i.test(url)) {
                return type === 'audio' ? 'audio/ogg' : 'video/ogg';
            } else if (/\.ogv/i.test(url)) {
                return 'video/ogg';
            } else if (/\.oga/i.test(url)) {
                return 'audio/ogg';
            } else if (/\.3gp/i.test(url)) {
                return 'audio/3gpp';
            } else if (/\.wav/i.test(url)) {
                return 'audio/wav';
            } else if (/\.aac/i.test(url)) {
                return 'audio/aac';
            } else if (/\.flac/i.test(url)) {
                return 'audio/flac';
            }

            // Let browser figure out if it can play it
            return '';
        }

        var ads = getUrlParameter('ads');
        ads = ads.replace(/~/g, '%');

        var defaultMedia = 'https://commondatastorage.googleapis.com/gtv-videos-bucket/sample/TearsOfSteel.mp4';
        
        var url = decodeURIComponent(getUrlParameter('file')) || defaultMedia;
        var media = document.createElement(type);
        media.id = 'media1';
        media.setAttribute('playsinline', true);
        media.autoplay = !!getUrlParameter('autoplay') || false;
        media.controls = true;
        media.playsinline = true;
        media.className = 'op-player__media';
        media.innerHTML = '<source src="' + url + '" type="' + getMimeType(url) + '">';
        document.getElementById('media').appendChild(media);

        var player = new OpenPlayer('media1', {
            ads: {
                src: ads || null,
            }
        });
        player.init();
    </script>
</body>

</html>
