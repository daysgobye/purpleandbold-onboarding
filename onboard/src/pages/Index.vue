<template>
<section id="contact">
    <div class="contact">
        <div class="Contact__title">
            <h2 class="section--header">on boarding</h2>
        </div>
        <div class="contact__body">
            <div class="flex__col contact__body__left">
                <div class="flex__col transback contact__body__left--name">
                    <label for="name">Name *</label>
                    <input type="text" v-model="messageData.yourName" name="name">
                </div>
                <div class="flex__col transback contact__body__left--company">
                    <label for="company">Company</label>
                    <input type="text" v-model="messageData.company" name="company">
                </div>
                
                <div class="flex__col transback contact__body__left--account">
                    <transition name="fade">
                        <div v-if="infoPopup.contact.on" class="infopopup">
                        {{ infoPopup.contact.message }}
                        </div>
                    </transition>
                    
                    <button class="info"
                    @click="popUp(infoPopup.contact,5000)"
                     >?</button>
                    <label for="company">Best way to get in contact </label>
                    <select v-model="messageData.contactAccout">
                      <option disabled value="">Please select one</option>
                      <option>Slack</option>
                      <option>discord</option>
                      <option>Email</option>
                      <option>Phone</option>
                      <option>skype</option>
                    </select>
                    <span v-show="messageData.contactAccout">
                      <label for="accountName">User name</label>
                      <br>
                      <input name="accoutName" type="text" v-model="messageData.contactAccoutUsername">
                    </span>
                </div>
                <div  class="flex__col transback contact__body__left--telephone">
                    <label for="Telephone">Telephone As Fall Back</label>
                    <input type="text" v-model="messageData.telephone" name="Telephone">
                </div>
                <div class="flex__col transback contact__body__left--email">
                    <label for="email">Email As Fall Back</label>
                    <input type="text" v-model="messageData.email" name="email">
                </div>
                <div class="flex__col transback contact__body__left--details">
                     <transition name="fade">
                        <div v-if="infoPopup.competer.on" class="infopopup">
                        {{ infoPopup.competer.message }}
                        </div>
                    </transition>
                    
                    <button class="info"
                    @click="popUp(infoPopup.competer,5000)"
                     >?</button>
                    <label> Competer web sites</label>
                    <div class="tag">
                       <div class="tag__bubbles" v-for="(tag, index) in comp" :key="index" >
                            <p>{{ tag}}</p>
                        </div>
                        <input type="text" placeholder="amazon.com" @keyup.enter="compTag" v-model="customComp"> 
                        <button @click="compTag">+</button>
                    </div>
                </div>
                  <div class="flex__col transback contact__body__left--details">
                       <transition name="fade">
                            <div v-if="infoPopup.inspiration.on" class="infopopup">
                            {{ infoPopup.inspiration.message }}
                            </div>
                     </transition>
                    
                    <button class="info"
                    @click="popUp(infoPopup.inspiration,5000)"
                     >?</button>
                    <label> Inspiration web sites</label>
                    <div class="tag">
                       <div class="tag__bubbles" v-for="(insp, index) in inspirationSite" :key="index" @click="addTag(index)">
                            <p>{{insp}}</p>
                        </div>
                        <input type="text" placeholder="purpleandbold.com" @keyup.enter="inspirationTag" v-model="customInspiration">
                         <button @click="inspirationTag">+</button>
                         <div class="flex__col">
                          <label for="inspnote">what is it that you like? about it </label>
                          <textarea name="inspnote" placeholder="eg I like the nav bar on this site" v-model="inspirationSiteNotes" id="" ></textarea>  
                         </div>
                        
                        
                    </div>
                </div>
                  <div class="flex__col transback contact__body__left--account">
                    <label for="company">Hosting </label>
                    <select v-model="hosting.option">
                      <option disabled value="">Please select one</option>
                      <option>I will Host it my self and I don't have hosting arangments</option>
                      <option>I will host it my self I and will take care of everything on my own </option>
                      <option>I will host it my self and give you logins to do it</option>
                      <option>I am planing on you Hosting it</option>
                      <option>I am not sure what Im going to do</option>
                    </select>
                    <span v-if="hosting.option == 'I will host it my self and give you logins to do it'">
                      <label for="username">User name: </label>
      
                      <input name="usernanm" type="text" v-model="hosting.username">
                      <br>
                      <label for="username">passWord: </label>
         
                      <input name="usernanm" type="text" v-model="hosting.passWord">
                    </span>
                </div>
            </div>
            <div class="flex__col contact__body__right">
            <div class="flex__col transback contact__body__left--details">
                 <transition name="fade">
                        <div v-if="infoPopup.goals.on" class="infopopup">
                        {{ infoPopup.goals.message }}
                        </div>
                    </transition>
                    
                    <button class="info"
                    @click="popUp(infoPopup.goals,5000)"
                     >?</button>
                    <label> Goals With Your Site</label>
                    <div class="tag">
                       <div class="tag__bubbles" v-for="(tag, index) in tags" :key="index" @click="addTag(index)">
                            <p>{{ tag }}</p>
                        </div>
                        <input type="text" placeholder="Enter Your Own" @keyup.enter="addCustomTag" v-model="customTag"> 
                        <button @click="addCustomTag">+</button>
                    </div>
                    <h4>Your Goals</h4>
                    <div class="tag">
                        <transition-group name="tags">
                        <div class="tag__bubbles" v-for="(tag, index) in messageData.pickedTags" :key="index" >
                            <p>{{ tag }}  </p><button @click="removeTag(index)" class="tag__bubbles--del">x</button>
                        </div>
                        </transition-group>
                    </div>
                </div>
                <div class="flex__col transback contact__body__left--color">
                     <transition name="fade">
                        <div v-if="infoPopup.colors.on" class="infopopup">
                        {{ infoPopup.colors.message }}
                        </div>
                    </transition>
                    
                    <button class="info"
                    @click="popUp(infoPopup.colors,5000)"
                     >?</button>
                    <label for="colors">Brand Colors</label>
                    <div class="color">
                      <div class="color__bubble" v-for="(color, index) in colors" :key="index" :style="{background:color}">
                    </div>
                    </div>
                    <div class="contact__body__left--input">
                      <input type="color" name="colors"  v-model="color">
                    <button @click="addCustomColor">+</button>
                    </div>
                    
                </div>
                <div class="flex__col transback contact__body__right--missed">
                     <transition name="fade">
                        <div v-if="infoPopup.old.on" class="infopopup">
                        {{ infoPopup.old.message }}
                        </div>
                    </transition>
                    
                    <button class="info"
                    @click="popUp(infoPopup.old,5000)"
                     >?</button>
                    <label for="oldSiteLink">Old Site Link</label>
                    <input type="text" v-model="oldSite" name="oldSiteLink">
                    <label for="oldSiteNote">What did You Like What Did you Not like</label>
                    <textarea name="oldSiteNote" placeholder="eg I liked the way the contact page looked on my old site" v-model="oldSiteNotes" id="" cols="30" rows=6></textarea>
                </div>
                 <div  class="flex__col transback contact__body__left--telephone">
                    <label for="logo">Do You have A logo?</label>
                   <input type="radio" id="yes" value="yes" v-model="logoRadio">
                        <label for="yes">yes</label>
                        
                        <input type="radio" id="no" value="no" v-model="logoRadio">
                        <label for="no">no</label>
                        <br>
                        <div v-if="logoRadio=='yes'"> <p>If you want to use it please email it to contact@purpleAndBold.com <br>
                        or you can past a link here  </p> 
                        <input type="text" v-model="logoLink" name="logoLink">
                        </div>
                </div>
                <div class="flex__col transback contact__body__right--missed">
                    <label for="missed">Did We Miss Anything?</label>
                    <textarea name="missed" v-model="messageData.missed" id="" cols="30" rows=6></textarea>
                </div>
            </div>
        </div> 
        <div class="contact__send">
            
        <form action="https://formspree.io/posting@purpleandbold.gq"
            method="POST">
            
            <textarea name="message" id="contact__send--message" ref="realmessage" cols="3" rows="1"></textarea>
            <input type="submit" ref="submit" value="Submit">
        </form>
    </div>
    </div>
</section>
</template>
<script>
export default {
  data() {
    return {
      messageData: {
        yourName: "",
        company: "",
        contactAccout: "",
        contactAccoutUsername: "",
        telephone: "",
        email: "",
        missed: "",
        pickedTags: []
      },
      infoPopup: {
        contact: {
          on: false,
          message:
            "just pick the accout you like to use the most. If the service you like is not in there then let us know in the did we miss any thing section and we will take care of it."
        },
        competer: {
          on: false,
          message:
            "give us as meny links to your competers as you like. This info will be used to better understand your busness and inderstr. To get a sence of norms and best practices "
        },
        inspiration: {
          on: false,
          message:
            "here you can tell us some thing you like eg 'link to xyz.com - I like the headder on this site and the use of color'. Links dont just have to be to websites you like, maybe a image link to a logo you like or, a link to somthing that gives the right 'vibe' to the reader "
        },
        goals: {
          on: false,
          message:
            "there is somthing you are hoping to achive with your website. Its not just a pritty pice of art with you name on it. This is where you can tell us what you are hoping to do with your site, this keeps us on the right path, that way the whole site can be molded around achiveing your goals"
        },
        colors: {
          on: false,
          message:
            " if you have certen colors you want us to work into the design, maybe to match your other branding, or just because you like them. here you can let us know"
        },
        old: {
          on: false,
          message:
            "if this is your first site great leave blank but if we are remaking your old site, might as well not mess up the stuff your old site did right, and better yet make sure we are not repeting old mastakes"
        }
      },
      inspirationSite: [],
      customInspiration: "",
      inspirationSiteNotes: "",
      inspirationSiteNotesArr: [],
      tags: ["Increase Sales", "Create A Easy Service For Customors"],
      customTag: "",
      comp: [],
      customComp: "",
      color: "#ff6797",
      colors: [],
      oldSite: "",
      oldSiteNotes: "",
      logoRadio: "no",
      logoLink: "",
      hosting: {
        option: "",
        username: "",
        passWord: ""
      }
    };
  },
  mounted() {
    this.blocksubmit();
  },
  methods: {
    // this is called when you click on one of the given tags and moves it into the message
    addTag(i) {
      this.messageData.pickedTags.push(this.tags[i]);
    },
    // this is called when you enter a custom tag and it will add it to the message
    addCustomTag() {
      this.messageData.pickedTags.push(this.customTag);
      this.customTag = "";
    },
    inspirationTag() {
      this.inspirationSite.push(this.customInspiration);
      this.customInspiration = "";
      this.inspirationSiteNotesArr.push(
        this.customInspiration,
        this.inspirationSiteNotes
      );
      this.inspirationSiteNotes = "";
    },
    compTag() {
      this.comp.push(this.customComp);
      this.customComp = "";
    },
    addCustomColor() {
      this.colors.push(this.color);
    },
    removeTag(i) {
      this.messageData.pickedTags.splice(i, 1);
    },
    // this is called from the watchers and all it does if take in all of the input fields and put them into the hidden text feild that is sent out
    pushMessage() {
      const message = `
      poststart
      <div id="message">
      name: ${this.messageData.yourName} 
      company: ${this.messageData.company} 
      contact Accout: ${this.messageData.contactAccout} 
      contact username: ${this.messageData.contactAccoutUsername} 
      competers websites: ${this.tags} 
      inspration sites: ${this.inspirationSiteNotesArr} 
      email: ${this.messageData.email}
      phone: ${this.messageData.telephone} 
      Goals: ${this.messageData.pickedTags}
      Brand colors : ${this.colors}
      Old Site Link: ${this.oldSite} 
      Old Site Notes: ${this.oldSiteNotes}
      Do They have a logo: ${this.logoRadio}
      logo Link If they Had One ${this.logoLink}
      Notes:${this.messageData.missed}

      </div>
      postend
      `;
      console.log(this.$refs.realmessage.value);
      this.$refs.realmessage.value = message;
      this.blocksubmit();
    },
    blocksubmit() {
      if (
        !this.messageData.yourName ||
        !this.messageData.telephone ||
        !this.messageData.email
      ) {
        this.$refs.submit.disabled = true;
      } else {
        this.$refs.submit.disabled = false;
      }
    },
    popUp(field, timeUp) {
      field.on = !field.on;
      setTimeout(() => {
        field.on = false;
      }, timeUp);
    }
  },

  filters: {
    comma: function(value) {
      if (!value) return "";
      return value.toLocaleString();
    }
  },
  watch: {
    //these watchers watch for a changes on the input fields and call the funcion to push it to the real text field
    "messageData.yourName": function() {
      this.pushMessage();
    },
    "messageData.company": function() {
      this.pushMessage();
    },
    "messageData.telephone": function() {
      this.pushMessage();
    },
    "messageData.email": function() {
      this.pushMessage();
    },
    "messageData.missed": function() {
      this.pushMessage();
    },
    "messageData.price": function() {
      this.pushMessage();
    },
    "messageData.pickedTags": function() {
      this.pushMessage();
    }
  },
  components: {}
};
</script>
<style lang="sass" scoped>
@import './normalize.scss'
@import './base.sass'
$gradient: linear-gradient(145deg, #FED766 0%,#ff6797 85%)
$inputback: #f7f3f3
$cardback: rgba(255, 255, 255, .4)
$inputColor: black
$maintextcolor: white
$disabled: #fc3a3a45

section
    width: 100%
    height: auto
    color: $maintextcolor
    // background-image: $gradient
    background: linear-gradient(135deg, rgba(31,234,214,1) 0%, rgba(10,230,226,1) 0%, rgba(31,234,214,1) 0%, rgba(13,201,129,1) 100%), url("https://www.transparenttextures.com/patterns/vaio.png") 
    // background-image: url("https://www.transparenttextures.com/patterns/vaio.png")
    font-family: "avenir", sans-serif
    display: flex
    justify-content: center
    align-items: center
    @include edgesnap
        padding: 20px
    @include tablet-phone
        height: auto
        padding: 10px

        
    .contact
        width: 1100px
        @include edgesnap
            width: 100%
        h2.section--header 
            color: white
            padding-bottom: 10px
            padding-left: 0px
        input:focus 
            outline: none
            box-shadow: 0px 0px 7px 1px rgba(250,177,245,1);//rgba(234,162,110,1);
        &__body
            display: flex
            justify-content: center
            justify-content: space-between
            @include tablet-phone
                flex-direction: column
            &__left, &__right 
                label 
                    margin-bottom: 7px
            &__left
                width: 48%
                justify-content: space-between
                @include tablet-phone
                    width: 100%
                select
                  border: none
                  background: none
                .tag 
                    div:nth-child(1)
                        margin-left: 0px
                    .tag__bubbles
                        display: inline-block
                        cursor: pointer
                        //this is the left tags
                        transition: all 1s ease-in-out
                        
                h4 
                    font-weight: $light
                    margin-top: 20px
                .contact__body__left--details
                    input 
                        width: 50%
                        color: $maintextcolor
                        &:focus
                            box-shadow: none
                    textarea
                        width: 100%
                      
                    .tag
                        display: flex
                        flex-direction: column

                    button
                        display: flex
                        justify-content: center
                        align-items: center
                        border: 1px solid $maintextcolor
                        border-radius: 100%
                        height: 1.4em
                        width: 1.4em
                        line-height: 10px
                        transform: translateY(25%)
                    h4
                        margin-bottom: 20px
                    p
                        text-align: center
              
            &__right
                dipslay: flex 
                flex-direction: column 
                justify-content: space-between
                width: 48%
                overflow: hidden
                @include tablet-phone
                    width: 100%
                &--missed 
                    margin-top: 15px
                .tag
                    min-height: 62px
                    flex-wrap: wrap
                    span
                        height: 100%
                    &__bubbles
                        height: 75%
                        cursor: pointer
                .tags-enter-active
                    animation: tag-in 1.5s forwards
                .tags-leave-active
                    animation: tag-out 2s forwards
                .tags-move
                    transition: all 2s
                .contact__body__left--color
                  .color
                    display: flex
                    flex-wrap: wrap
                    &__bubble
                      width: 30px
                      height: 30px
                      border-radius: 100%
                      border: 1px solid $maintextcolor
                  .contact__body__left--input
                    display: flex
                    button
                      transform: translateY(0)
                  button
                    display: flex
                    justify-content: center
                    align-items: center
                    border: 1px solid $maintextcolor
                    border-radius: 100%
                    height: 1.4em
                    width: 1.4em
                    line-height: 10px
                    transform: translateY(25%)
            .flex__col
                display: flex
                flex-direction: column
            .info
                border: 1px solid white 
                color: gray
                border-radius: 100%
                margin-bottom: 5px
                width: 25px !important
                height: 25px !important

            .pb
                padding-bottom: 64px
            .transback
                background: $cardback
                padding: 10px
                margin-bottom: 20px
                border-radius: 3px
            input
                color: $inputColor
                border: none
                background: $inputback
                font-size: 1.1rem
                padding: 6px
            textarea
                border: none
                background: $inputback
                margin-top: 8px 
                color: $inputColor
                resize: none
                padding: 2px
                &:focus 
                    outline: none
                    box-shadow: 0px 0px 7px 1px rgba(250,177,245,1);//rgba(234,162,110,1);
        .infopopup
            position: absolute
            padding: 5px
            background: rgba(40, 40, 40, 0.61)
            width: 30%
            transform: translateY(-100%)
            @include edgesnap
                width: 100%
        .fade-enter-active, .fade-leave-active 
            transition: opacity 1s
        .fade-enter, .fade-leave-to 
            opacity: 0;
                        
        .tag
            display: flex
            flex-wrap: wrap
            span
                display: flex
                flex-wrap: wrap 
            input
                background: none
                border-bottom: 2px solid white 
                &::placeholder
                    color: $maintextcolor
            &__bubbles
                display: flex
                cursor: bubbles
                background: $cardback
                border-radius: 15px
                padding: 4px 15px
                margin: 5px
                font-size: 0.9em
                .tag__bubbles--del
                    cursor: pointer
                    height: 1.25rem
                    width: 1.25rem
                    display: flex
                    justify-content: center
                    align-items: center
                    border: 1px solid white
                    border-radius: 100%
                    margin-right: 2px
        &__send
            display: flex
            justify-content: flex-end
            align-self: flex-end
            input
                display: flex 
                flex-direction: column 
                justify-content: center
                align-items: center
                color: $maintextcolor
                height: 45px
                width: 160px
                border: .08em solid $maintextcolor
                border-radius: 3px
                font-size: .9em
                letter-spacing: .05em
                font-weight: $light
                margin-bottom: 40px
                transition: all 0.3s ease-in-out
                @include tablet-portrait
                    font-size: .85em
                    height: 36px 
                    width: 145px
                @include phone-large 
                    margin-bottom: 30px
                @include phone-small 
                    margin-bottom: 20px
                &:hover 
                    transform: scale(1.03) translateY(-3px)
                &:disabled
                    background: $disabled
                    box-shadow: 0px 0px 5px 0px $disabled
                    animation: disabled 3s infinite
                    &:hover 
                        transform: scale(1) translateY(0px)
            #contact__send--message
                visibility: hidden
@keyframes tag-in 
    0%    
        // transform: translatex(-300%)
        opacity: 0
    100%  
        // transform: translatex(0%)
        opacity: 1
@keyframes tag-out 
    0%    
        // transform: translatex(0%)
        opacity: 1
    100%  
        // transform: translatex(-500%)
        opacity: 0
@keyframes disabled 
    0%    
        opacity: 1
    50%  
        opacity: .4
    100%
        opacity: 1 
.tags-enter, 
  opacity: 1
  //transform: translateY(300px)
.tags-leave-to
  opacity: 0
.tags-leave-active 
  //position: absolute
  opacity: 0
  //transform: translateX(-1800px) scale(0.3)
  //right: 0
</style>