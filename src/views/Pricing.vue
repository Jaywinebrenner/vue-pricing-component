<template>

<div class="wrapper">

  <div class="buttonWrapper">

      <button 
      @click="currentFrequency = 'monthly'"
      class="button"
      :class="currentFrequency == 'monthly' ? 'buttonSelected' : ''">
      MONTHLY
      </button>

      <button 
      @click="currentFrequency = 'yearly'" 
      class="button" 
      :class="currentFrequency == 'yearly' ? 'buttonSelected' : ''"
      >
      YEARLY
      </button>

  </div>

<div class="wholeBenefitWrapper">
    <div v-for="plan in plans" class="benefitWrapper" :key="plan.id">
      <h3 
      v-for="benefit in plan.benefits[currentFrequency]" :key="benefit.id">{{benefit}}</h3>

    


      <div class="priceWrapper">
        <div class="priceText">${{plan.pricing[currentFrequency].price}}</div>
        <div class="monthText">{{plan.pricing[currentFrequency].label}}</div>
      </div>

    </div>
  </div>


</div>
  
</template>



<script>
export default {


  data: function() {

    return {
      currentFrequency: 'monthly',

      plans: [
        {
          benefits: {
            monthly: ["Benefit 1", "Benefit 2", "Benefit 3"],
            yearly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
          },
          pricing: {
            monthly: { price: 99, label: "/mo"},
            yearly: { price: 499, label: "/yr"},
          }
        },
        {
          benefits: {
            monthly: ["Benefit 1", "Benefit 2", "Benefit 3"],
            yearly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
          },
          pricing: {
            monthly: { price: 199, label: "/mo"},
            yearly: { price: 999, label: "/yr"},
          }
        },
        {
          benefits: {
            monthly: ["Benefit 1", "Benefit 2", "Benefit 3"],
            yearly: ["Benefit 1", "Benefit 2", "Benefit 3", "Benefit 4"],
          },
          pricing: {
            monthly: { price: 299, label: "/mo"},
            yearly: { price: 1399, label: "/yr"},
          }
        }
      ]

    }
  }

}
</script>




<style lang="stylus" scoped>

</style>