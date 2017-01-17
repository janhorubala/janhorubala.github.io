---
layout: clean
---

<link rel="stylesheet" type="text/css" href="{{ site.url }}/assets/deviant/deviantART-gallery.min.css"/>
<link rel="stylesheet" type="text/css" href="{{ site.url }}/assets/deviant/css/jTinder.css">
<style>
    .spinner {
      width: 40px;
      height: 40px;

      position: absolute;
      left: calc(50% - 20px);
        top: calc(50% - 20px);
      margin: 0;
    }

    .double-bounce1, .double-bounce2 {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #333;
      opacity: 0.6;
      position: absolute;
      top: 0;
      left: 0;
      
      -webkit-animation: sk-bounce 2.0s infinite ease-in-out;
      animation: sk-bounce 2.0s infinite ease-in-out;
    }

    .double-bounce2 {
      -webkit-animation-delay: -1.0s;
      animation-delay: -1.0s;
    }

    @-webkit-keyframes sk-bounce {
      0%, 100% { -webkit-transform: scale(0.0) }
      50% { -webkit-transform: scale(1.0) }
    }

    @keyframes sk-bounce {
      0%, 100% { 
        transform: scale(0.0);
        -webkit-transform: scale(0.0);
      } 50% { 
        transform: scale(1.0);
        -webkit-transform: scale(1.0);
      }
    }
</style>
<div style="max-width: 600px; min-width: 320px; margin: auto">
    <!-- start padding container -->
    <div id="progress"></div>

    <div class="wrap">
        <!-- start jtinder container -->
        <div id="tinderslide">
            <ul id="gallery">
                <div class="spinner">
                  <div class="double-bounce1"></div>
                  <div class="double-bounce2"></div>
                </div>
            </ul>
        </div>
        <!-- end jtinder container -->
    </div>
    <!-- end padding container -->

    <!-- jTinder trigger by buttons  -->
    <div class="actions">
        <a href="#" class="dislike"><i class="btn-dislike"></i></a>
        <a href="#" class="like"><i class="btn-like"></i></a>
    </div>

    <!-- jQuery lib -->
<script type="text/javascript" src="{{ site.url }}/assets/deviant/js/jquery.min.js"></script>
<!-- transform2d lib -->
<script type="text/javascript" src="{{ site.url }}/assets/deviant/js/jquery.transform2d.js"></script>
<!-- jTinder lib -->
<script type="text/javascript" src="{{ site.url }}/assets/deviant/js/jquery.jTinder.js"></script>
<!-- jTinder initialization script -->
<script type="text/javascript" src="{{ site.url }}/assets/deviant/ProgressBar.js"></script>


<script type="text/javascript" src="{{ site.url }}/assets/deviant/deviantART-gallery-plugin.js"></script>

<script type="text/javascript">
    function photos(url, id, ratio) {
    return new Promise((res, rej) => {

      // thanks http://stackoverflow.com/a/7369516/1696757
      var s = document.createElement('script');
      s.src = "http://query.yahooapis.com/v1/public/yql?q=" + escape('select * from xml where url="' + url + '"') + "&_maxage=86400&format=json&callback=callback";
      document.body.appendChild(s);
      
      window['callback'] = callback;
      function callback(feed) {
          var deviations = [];
          console.log(url, feed);
          var items = feed.query.results.rss.channel.item;

          for(var i = 0, l = items.length; i < l; i++) {
              var object = {};

              object.title = items[i].title[0];
              object.image = items[i].content.url;

              deviations.push(object);
          }
          res(deviations)
      }

    })
}

var url1 = 'http://backend.deviantart.com/rss.xml?type=deviation&q=by:6artificial6';
var url2 = 'http://backend.deviantart.com/rss.xml?type=deviation&q=boost:popular/in:photography';
photos(url1)
.then(photo1 => {
  photos(url2)
  .then(photo2 => {
    const u1 = shuffle(photo1);
    const u2 = shuffle(photo2);
    const image = (img, numb) => (`<li class="${numb}">` + 
	    `<div class="img" style="background: url('${img}') no-repeat scroll center center; background-size: contain"></div>` + 
	    `<div class="dislike"></div>` + 
	    `<div class="like"></div>` + 
    	`</li>`)

    var len = u1.length + u2.length < 50 ? u1.length + u2.length : 50;
    var result = '';
    for (let i = 0; i < len; i++) {
      const numb = Math.floor(Math.random() * 2) + 1
      if (numb === 1) {
        if (u1.length > 0) {
          result += image(u1.pop().image, 1)
        } else {
          result += image(u2.pop().image, 2)
        }
      } else {
        if (u2.length > 0) {
          result += image(u2.pop().image, 2)
        } else {
          result += image(u1.pop().image, 1)
        }        
      }
    }

window.onload = function onLoad() {
    $('#gallery').html(result);
    runTinder();
}
   })
})

window['counter_good'] = 0;
window['counter_bad'] = 0;

function runTinder() {
  $("#tinderslide").jTinder({
    // dislike callback
      onDislike: function (item) {
        // set the status text
  		console.log('should be 2: ')
        console.log(item.attr('class'));
        if (item.attr('class') == 2) {
        	counter_good += 1
        } else {
        	counter_bad += 1
        }
        bar.set(counter_good / (counter_good + counter_bad))

          // $('#status').html('Dislike image ' + (item.index()+1));
      },
    // like callback
      onLike: function (item) {
      	console.log('should be 1: ')
        console.log(item.attr('class'));
        if (item.attr('class') == 1) {
        	counter_good += 1
        } else {
        	counter_bad += 1
        }
        // set the status text
          // $('#status').html('Like image ' + (item.index()+1));
        bar.set(counter_good / (counter_good + counter_bad))
      },
    animationRevertSpeed: 200,
    animationSpeed: 400,
    threshold: 1,
    likeSelector: '.like',
    dislikeSelector: '.dislike'
  });

  /**
   * Set button action to trigger jTinder like & dislike.
   */
  $('.actions .like, .actions .dislike').click(function(e){
    e.preventDefault();
    $("#tinderslide").jTinder($(this).attr('class'));
  });
}

window['bar'] = new ProgressBar.Line('#progress', {
  strokeWidth: 4,
  easing: 'easeInOut',
  duration: 1400,
  color: '#FFEA82',
  trailColor: '#eee',
  trailWidth: 1,
  svgStyle: {width: '100%', height: '100%'},
  text: {
    style: {
      // Text color.
      // Default: same as stroke color (options.color)
      color: '#999',
      position: 'absolute',
      right: '0',
      top: '30px',
      padding: 0,
      margin: 0,
      transform: null
    },
    autoStyleContainer: false
  },

  from: {color: '#ED6A5A'},
  to: {color: '#5cb85c'},
  step: (state, bar) => {
    bar.setText(Math.round(bar.value() * 100) + ' %');
    bar.path.setAttribute('stroke', state.color);
  }
});

bar.text.style.fontFamily = '"Raleway", Helvetica, sans-serif';
bar.text.style.fontSize = '18px';
bar.text.style.right = '20px';
bar.animate(0);  // Number from 0.0 to 1.0


function shuffle(array) {
  var currentIndex = array.length, temporaryValue, randomIndex;

  // While there remain elements to shuffle...
  while (0 !== currentIndex) {

    // Pick a remaining element...
    randomIndex = Math.floor(Math.random() * currentIndex);
    currentIndex -= 1;

    // And swap it with the current element.
    temporaryValue = array[currentIndex];
    array[currentIndex] = array[randomIndex];
    array[randomIndex] = temporaryValue;
  }

  return array;
}
</script>
</div>
