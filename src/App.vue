<template>
  <v-app>
    <v-toolbar fixed app :clipped-left="clipped">
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-btn icon @click.stop="miniVariant = !miniVariant">
        <v-icon v-html="miniVariant ? 'chevron_right' : 'chevron_left'"></v-icon>
      </v-btn>
      <v-btn icon @click.stop="clipped = !clipped">
        <v-icon>web</v-icon>
      </v-btn>
      <v-btn icon @click.stop="fixed = !fixed">
        <v-icon>remove</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title"></v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>menu</v-icon>
      </v-btn>
    </v-toolbar>
    <v-spacer></v-spacer>
    <v-content>
      <v-container grid-list-md text-xs-center>
          <v-layout row wrap>
            <template>
              <v-flex xs12 sm6 offset-sm3>
                <v-card dark color="grey darken-1">

                  <v-form v-model="valid" >

                    <v-card-title>Blog Post:</v-card-title>

                    <v-text-field
                      label="Title"
                      v-model="blogtitle"
                      placeholder="Add a Blog Title"
                      :rules="titleRules"
                      :counter="10"
                      required
                      name="blogtitle"
                    ></v-text-field>

                    <v-text-field
                      label="Post"
                      v-model="blogpost"
                      placeholder="Add the Post"
                      :rules="postRules"
                      :counter="30"
                      required
                      name="blogpost"
                    ></v-text-field>

                    <v-text-field
                      label="Posted"
                      v-model="blogposted"
                      placeholder="Today - Time"
                      disabled
                      name="blogposted"
                      max="15"
                    ></v-text-field>
                    <v-card-actions >
                      <v-btn @click="submit"  :disabled="!valid" color="grey lighten-1">submit</v-btn>
                      <v-btn @click="clear" color="grey lighten-1">clear</v-btn>
                    </v-card-actions>
                  </v-form>
                </v-card>
              </v-flex>

            </template>
          </v-layout>
        </v-container>

        <v-container grid-list-md text-xs-center>
            <v-layout row wrap>
              <template>
                <v-flex xs12 sm6 offset-sm3>
                  <v-card dark color="grey darken-1">
                    <v-card-title>Blog Post List:</v-card-title>
                    <v-form>
                      <ul>

                        <li v-for="(item, index) in itemls" >

                            <v-card-text>Title: {{  item.title }}  </v-card-text>
                            <v-card-text>Post: {{  item.post }} </v-card-text>
                            <v-card-text>Posted: {{  item.posted }} </v-card-text>

                          <v-card-actions>
                             <v-btn @click="removeit(index)" color="grey lighten-1"> Delete </v-btn>
                             <v-btn @click="editit(index)" color="grey lighten-1"> Edit </v-btn>
                          </v-card-actions>
                        </li>

                      </ul>
                    </v-form>

                  </v-card>
                </v-flex>
                </template>
            </v-layout>

        </v-container>
    </v-content>

    <v-footer :fixed="fixed" app>
      <span>&copy; 2017</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    data () {
      return {
        clipped: false,
        miniVariant: false,
        drawer: true,
        fixed: false,
        items: [ ],
        title: "Blog of Lee's Training",
        blogtitle: '',
        blogpost: '',
        blogposted: '',
        blogedit: 0,
        blogtitle: '',
        valid: false,
        titleRules: [
          (v) => !!v || 'Title is required',
          (v) => v.length <= 10 || 'Title must be less than 10 characters'
        ],
        postRules: [
          (v) => !!v || 'Post is required',
          (v) => v.length <= 30 || 'Post must be less than 30 characters'
        ],
        formdate: new Date().toLocaleString(),
        itemls:  [{ title: 'Or Not', post: ' This maybe okay ', posted: 'Today - Time'}]
      }
    }
  ,
  methods: {
    submit() {
      //console.log(this.formdate);
      if(this.blogedit > 0){
         //this.itemls.splice(this.blogedit, 1,this.blogredux)
         this.itemls[this.blogedit].title = this.blogtitle;
         this.itemls[this.blogedit].post = this.blogpost;
         this.itemls[this.blogedit].posted = this.formdate;
      }else{
        this.itemls.push({
          title: this.blogtitle,
          post: this.blogpost,
          posted: this.formdate
        })
      }
      this.blogtitle = '';
      this.blogpost = '';
      this.blogposted = this.formdate;
    },
    clear() {
        this.blogtitle = '';
        this.blogpost = '';
      
    },
    removeit(index) {
      this.itemls.splice(index, 1);
    }
    ,
    editit(index) {
      this.blogtitle = this.itemls[index].title;
      this.blogpost = this.itemls[index].post;
      this.blogposted = this.itemls[index].posted;
      this.blogedit = index;
    }
  }
  }
</script>
