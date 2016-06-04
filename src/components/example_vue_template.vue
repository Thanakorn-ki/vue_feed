<template>

  <div class='example'>{{ msg }}</div> <br>
  <div class="ui center aligned container">
    <div class="ui two column divided grid">
      <div class="row">
        <div class="six wide column">
          <div class="ui segment">
            2
          </div>
        </div>
        <div class="ten wide column">
          <div class="ui segment">
            <div class="ui input">


                  <input type="text" placeholder="What is your mind?" v-model="status">


                  <div class="ui animated button" tabindex="0" v-on:click="addPost(status)">
                    <div class="visible content">POST</div>
                    <div class="hidden content">
                      <i class="right arrow icon"></i>
                    </div>
                  </div>


            </div>
          </div>
          <div v-for="tmp in data" class="centered">
                <div class="ui card" style="width:100%;margin-bottom:14px;">
                <div class="content">
                  <div class="right floated meta">{{formatdate(tmp.date)}}</div>
                  <img class="ui avatar image" src="/static/{{tmp.pic}}"> {{tmp.name}}
                </div>
                <div class="image">
                  <img>
                </div>
                <div class="content">
                  {{tmp.message}}
                  <span class="right floated">
                    <i class="heart outline like icon"></i>
                    {{tmp.love.length}} likes
                  </span>
                </div>
                <div class="extra content">
                  <div class="ui comments">
                      <h3 class="ui dividing header">Comments</h3>
                      <div class="comment">
                        {{formatdate(tmp.date)}}
                        <div class="content" v-for="comment in tmp.comment">
                          <a class="author">{{comment.name}}</a>
                          <div class="metadata">
                            <span class="date">{{formatdate(comment.date)}}</span>
                          </div>
                          <div class="text">
                          {{comment.message}}
                          </div>
                        </div>
                      </div>

                      <form class="ui reply form">
                        <div class="field">
                          <textarea v-model="tmp.newComment"></textarea>
                        </div>

                        <div class="ui blue labeled submit icon button" v-on:click="addcomment($index, tmp.newComment)">
                          <i class="icon edit"></i> Add Reply
                        </div>
                      </form>
                    </div>
                </div>
              </div>
          </div>
        </div>
      </div>
  </div>
</div>


</template>

<script>
/* global moment*/
var data = [
  {
    name: 'Alejandro G. Iñárritu',
    pic: 'a.png',
    date: 1464940250515,
    message: 'Best Director winner',
    newComment: '',
    love: [
      'jamie',
      'vardy',
      'Leonardo',
      'Leonardo',
      'Leonardo'
    ],
    comment: [
      {
        name: 'Leonardo DiCaprio',
        pic: 'b.jpg',
        date: 1464940250515,
        message: 'congratulation boy!!'
      },
      {
        name: 'Adam McKay',
        pic: 'c.jpg',
        date: 1464940250515,
        message: 'good job!!'
      }
    ]
  },
  {
    name: 'Ennio Morricone',
    pic: 'b.png',
    date: 1464940250515,
    message: 'Best Original Score winner',
    newComment: '',
    love: [
      'jamie',
      'vardy',
      'Leonardo',
      'Leonardo',
      'Leonardo'
    ],
    comment: [
      {
        name: 'Alejandro G. Iñárritu',
        pic: 'b.jpg',
        date: 1464940250515,
        message: 'excellent!!'
      },
      {
        name: 'jamie vardy',
        pic: 'c.jpg',
        date: 1464940250515,
        message: 'why you so good!!'
      }
    ]
  }
]
export default {
  data () {
    return {
      msg: 'Thanakorn!',
      data: data
    }
  },
  methods: {
    addPost: function (status) {
      var tempStatus = {
        name: 'Alejandro',
        pic: 'a.png',
        date: {type: Date, defualt: Date.now},
        message: status,
        newComment: '',
        love: [],
        comment: []
      }
      this.data.push(tempStatus)
      this.status = ''
    },
    addcomment: function (index, input) {
      var str = {
        name: this.msg,
        pic: 'ab.png',
        date: {type: Date, defualt: Date.now},
        message: input
      }
      this.data[index].comment.push(str)
      data[index].newComment = ''
    },
    formatdate: function (time) {
      return moment(time).startOf('day').fromNow()
    }
  }
}
</script>
<style>
.example {
  color: red;
}
</style>
