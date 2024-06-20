<template>
  <div>
    <page-title>Color</page-title>
    <p>You've picked a great color!</p>
    <flask-item class="flask__result" :color="mixtureEffectFill" :amount="100" :size="15"/>
    <div class="share-link">
      <i class="pi pi-share-alt"></i>
      <input type="text" :value="shareUrl" readonly />
    </div>
  </div>
</template>

<script>
import FlaskItem from '@/components/shared/FlaskItem.vue';
import PageTitle from '@/components/PageTitle.vue';

export default {
  name: 'ColorShare',
  components: {
    FlaskItem,
    PageTitle
  },
  props: {
    red: {
      type: Number,
      required: false,
      default: null
    },
    green: {
      type: Number,
      required: false,
      default: null
    },
    blue: {
      type: Number,
      required: false,
      default: null
    }
  },
  computed: {
    mixtureEffectFill () {
      return `rgb(${this.red}, ${this.green}, ${this.blue})`;
    },
    shareUrl () {
      return `${window.location.origin}/color/${this.red}/${this.green}/${this.blue}`;
    }
  },
  beforeMount() {
    this.validateParams();
  },
  methods: {
    validateParams() {
      const { red, green, blue } = this.$route.params;
      if (
        red === undefined || green === undefined || blue === undefined ||
        isNaN(red) || isNaN(green) || isNaN(blue) ||
        red < 0 || green < 0 || blue < 0 ||
        red > 255 || green > 255 || blue > 255
      ) {
        this.$router.replace('/');
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.flask__result {
  margin: 20px auto;
}

.share-link {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 20px;
}
.share-link input {
  width: calc(100% - 2rem);
  padding: 10px;
  font-size: 1rem;
  text-align: center;
  border: 1px solid #ddd;
  border-radius: 0.5rem;
}

.share-link i {
  font-size: 1.5rem;
  color: #637892;
  margin-right: 1rem;
}
</style>
