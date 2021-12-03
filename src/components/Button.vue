<template>
  <button class="btn"><i class="fas fa-arrow-left"></i> Back</button>
</template>

<style lang="scss" scoped>
.btn {
  margin: 3rem 0 6rem;
  padding: 1rem 2rem;
  background: $color-white;
  outline: none;
  border: none;
  border-radius: 0.5rem;
  box-shadow: -1px 1px 2px 1px rgba($color-black, 0.1);

  @include respond(lap) {
    margin: 8rem 0;
    padding: 1.2rem 3rem;
    font-size: 1.4rem;
  }

  i {
    margin-right: 1rem;
  }
}
</style>
