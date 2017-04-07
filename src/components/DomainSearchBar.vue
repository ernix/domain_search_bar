<template>
  <div class="domain-search-bar">
    <form>
      <input name="domain" type="text" />
      <button name="submit" type="submit">search</button>
    </form>
  </div>
</template>

<script>
import Result from './Result'

export default {
  name: 'domain-search-bar',
  components: {
    Result
  },
  data () {
    return {
      next: '',
      list: []
    }
  }
}
/*
(function ($) {
  'use strict';

  $(function () {
    var line = $('#line').html();

    $('#register').submit(function (e) {
      e.preventDefault();

      var label = punycode.toASCII(this.domain.value.replace(/^\s*|\s*$/, "", "g"));
      var re_label = /^(.*)\.earth$/i;
      var m = re_label.exec(label);
      if (m !== null) {
        label = m[1];
      }

      $('#result').prepend(_.template(line)({label: label}));

      $('#result div.unresolve').each(function () {
        var self = $(this);

        if (label === '') {
          self.append('<span>Submit a domain</span>');
          self.removeClass('unresolve');
          return false;
        }

        var timer;
        var domain = self.data('domain');
        $.ajax({
          dataType: 'jsonp',
          async: true,
          cache: false,
          url: 'http://domain.earth/domain_search/earth.cgi',
          jsonp: 'callback',
          data: { domain: label },
          beforeSend: function () {
            var dom = $('<span style="width:4em;">'), dots = '.';
            timer = setInterval(function () {
              dots = (dots.length > 2) ? '' : dots + '.';
              dom.text(dots);
            }, 500);
            self.find('span').append(dom);
          }
        })
        .done(function (data) {
          if (data === null || data.status !== '0') {
            self
              .find('span')
              .addClass('text-warning')
              .addClass('btn')
              .html('Unavailable');
            return true;
          }

          if (data.hasOwnProperty('premium') && data.premium === '1') {
            self
              .find('span')
              .addClass('text-warning')
              .addClass('btn')
              .html('Premium');
            return true;
          }

          $('#partners a').each(function () {
            var uri = $(this).uri();
            uri.setQuery({'domain': domain});
          });

          $('#partners').slideDown();

          var text = 'Available!';

          self
            .find('span')
            .html(
              $('<span>').addClass('text-success').addClass('btn')
                .css('font-size', 'large')
                .text(text)
            );

          return true;
        })
        .fail(function () {
          self
            .find('span')
            .addClass('text-warning')
            .addClass('btn')
            .html('Unavailable');
          return true;
        })
        .always(function () {
          clearInterval(timer);
        });

        self.removeClass('unresolve');
      });
    });
  });
})(jQuery);
*/
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
</style>
