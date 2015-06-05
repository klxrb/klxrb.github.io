---
layout: article
title: "RubyMY Slack Invitation"
date: 2015-06-04T17:33:00+08:00
modified:
excerpt:
image:
  feature:
  teaser:
  thumb:
ads: false
---

Good news everyone! We're on <i class="fa fa-slack"></i>Slack @ <a href="https://rubymy.slack.com">https://rubymy.slack.com</a>!

<strong>Invite yourself to our <a class="icon" href="https://rubymy.slack.com"><i class="fa fa-slack"></i>Slack</a> group!</strong>

<form id="slack_invite">
  Email: <input type="email" name="email_invite" id="email_invite" placeholder="please@invite.me">
  <button id="submit_button" type="submit"><span>Submit</span><i class="fa fa-spinner fa-spin hidden"></i></button>
  <span id="error_notice"></span>
  <span id="status_notice"></span>
</form>


<script>
$(function(){
  $('#slack_invite').submit(function(){
    function disable_submit(){
      $('#submit_button').prop('disabled',true).addClass('disabled');
      $('#submit_button span').addClass('hidden');
      $('#submit_button i').removeClass('hidden');
    }

    function restore_submit(){
      $('#submit_button').prop('disabled',false).removeClass('disabled');
      $('#submit_button span').removeClass('hidden');
      $('#submit_button i').addClass('hidden');
    }

    error = false;

    $('#status_notice, #error_notice').html('');

    disable_submit();
    
    if(!$('#email_invite').val().trim()){
      $('#error_notice').html('Please enter a valid email.')
      restore_submit();
      error = true
    }

    if(!error){
      $.ajax({
        url: 'https://rubymy-slack-invite.herokuapp.com/invite.json',
        dataType: 'jsonp',
        data: {
          email: $('#email_invite').val()
        },
        success: function(data){
          if(data.ok){
            $('#error_notice').html('');
            $('#status_notice').html('Invitation Email Sent :)');
          }else{
            $('#error_notice').html('Error: ' + data.error.replace(/_/g, ' ') + '.');
            $('#status_notice').html('');
          }
        },
        complete: function(data){
          restore_submit();
        }
      })
    }
    
    return false;
  })
})
</script>