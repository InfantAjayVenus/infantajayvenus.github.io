**Tags**: #web-dev 

---
```javascript
{
    initApp: function() {
        $('#logout').on('click', $$.logout);
        $('#catch').html($$.today);
        $$.getCookie();
        $$.dataload();
        window.addEventListener('devicemotion', $$.onDeviceMotion);
    },
    rendar: function() {
        $('#count').html($$.count.toLocaleString() + '<span>step</span>');
    },
    onDeviceMotion: function(e) {
        e.preventDefault();
        var ag = e.accelerationIncludingGravity;
        var acc = Math.sqrt(ag.x * ag.x + ag.y * ag.y + ag.z * ag.z);
        if ($$.ismove) {
            if (acc < 9.8) {
                $$.count++;
                $$.ismove = false;
                $$.setCookie();
                $$.rendar();
            }
        } else {
            if (acc > 12) {
                $$.ismove = true;
            }
        }
    },
    dataload: function() {
        var showlist = function(data) {
            var detail = [];
            if (data) detail = data.split('\t');
            var cnt = parseInt(detail.length);
            var updateflg = true;
            var tr;
            if (cnt !== 0) {
                $.each(detail, function(i, val) {
                    var v = val.split(',');
                    if (v.length === 2) {
                        tr = $('<tr>');
                        tr.append($('<td>').text(v[0]));
                        tr.append($('<td>').text(v[1].toLocaleString() + ' steps'));
                        $('#result').prepend(tr);
                        if (v[0] == $$.p_today) updateflg = false;
                        $$.list.push(val);
                    }
                });
            }
            if ($$.p_today === '' || $$.p_count === 0) updateflg = false;
            if (updateflg) {
                if ($$.p_today != $$.today) {
                    $$.list.push($$.p_today + ',' + $$.p_count);
                    u.setServerPersonal($$.list.join('\t'), function(data) {
                        tr = $('<tr>');
                        tr.append($('<td>').text($$.p_today));
                        tr.append($('<td>').text($$.p_count.toLocaleString() + ' steps'));
                        $('#result').prepend(tr);
                    });
                }
            }
        };
        u.getServerPersonal(showlist);
    },
    setCookie: function() {
        var cdata = {
            today: $$.today,
            count: parseInt($$.count)
        };
        u.setCookie(cdata);
    },
    getCookie: function() {
        var cdata = u.getCookie();
        if (cdata) {
            if (cdata.today) $$.p_today = cdata.today;
            if (!isNaN(cdata.count)) $$.p_count = parseInt(cdata.count);
            $$.count = $$.today != $$.p_today ? 0 : $$.p_count;
            $$.rendar();
        }
    },
};
