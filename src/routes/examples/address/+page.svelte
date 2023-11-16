<script>
  import { Elements, Address } from '$lib'
  import { loadStripe } from '@stripe/stripe-js'
  import { PUBLIC_STRIPE_KEY } from '$env/static/public'
  import { onMount } from 'svelte'

  let stripe = null

  onMount(async () => {
    stripe = await loadStripe(PUBLIC_STRIPE_KEY)
  })
</script>

{#if stripe}
  <Elements {stripe} locale="en">
    <Address
      mode="shipping"
      allowedCountries={['pl']}
      fields={{
        phone: 'always'
      }}
      defaultValues={{
        phone: '',
        firstName: 'Jakie',
        lastName: 'Smith',
        address: {
          line1: 'test',
          line2: 'test',
          city: 'New York',
          postal_code: '00-000',
          country: 'pl'
        }
      }}
      display={{
        name: 'split'
      }}
      validation={{
        phone: {
          required: 'always'
        }
      }}
      on:ready={(e) => {
        console.log('ready')
      }}
      on:change={(e) => console.log(e)}
    />
  </Elements>
{/if}
