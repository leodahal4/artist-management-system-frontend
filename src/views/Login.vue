<template>
  <v-main>
    <v-container fill-height fluid>
      <v-row align="center" justify="center" class="mt-16">
        <v-col>
          <v-hover>
            <template v-slot:default="{ isHovering, props }">
              <v-card
                class="mx-auto"
                max-width="344"
                v-bind="props"
                :loading="isActive"
                :elevation="isHovering ? 10 : 2"
              >
                <template v-slot:loader="{ isActive }">
                  <v-progress-linear
                    :active="isActive"
                    color="blue"
                    height="3"
                    indeterminate
                  ></v-progress-linear>
                </template>

                <v-card-item>
                  <div>
                    <div class="text-overline mb-1 text-center">Login</div>
                    <v-text-field
                      :class="{ error: v$.username.$errors.length }"
                      variant="outlined"
                      v-model="username"
                      clearable
                      :color="isActiveTextFieldUsername"
                      @click="setTextFieldActive(1)"
                      prepend-inner-icon="mdi-account"
                      label="Email"
                    />
                    <div
                      class="input-errors text-red text-caption mt-n4 mb-3"
                      v-for="error of v$.username.$errors"
                      :key="error.$uid"
                    >
                      <div class="error-msg">{{ error.$message }}</div>
                    </div>

                    <v-text-field
                      :class="{ error: v$.password.$errors.length }"
                      variant="outlined"
                      v-model="password"
                      :color="isActiveTextFieldPassword"
                      @click="setTextFieldActive(2)"
                      prepend-inner-icon="mdi-account-key-outline"
                      label="Password"
                      type="password"
                    />
                    <div
                      class="input-errors text-red text-caption mt-n5"
                      v-for="error of v$.password.$errors"
                      :key="error.$uid"
                    >
                      <div class="error-msg">{{ error.$message }}</div>
                    </div>
                  </div>
                </v-card-item>

                <v-card-actions>
                  <v-btn
                    prepend-icon="mdi-cancel"
                    class="left"
                    variant="text"
                    @click="clear"
                  >
                    Clear
                  </v-btn>
                  <v-spacer></v-spacer>
                  <v-btn
                    prepend-icon="mdi-login"
                    class="right"
                    variant="text"
                    @click="login"
                  >
                    Login
                  </v-btn>
                </v-card-actions>
              </v-card>
            </template>
          </v-hover>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
import { useVuelidate } from "@vuelidate/core";
import { required, email } from "@vuelidate/validators";
export default {
  setup() {
    return { v$: useVuelidate() };
  },
  data() {
    return {
      isActive: false,
      username: "",
      password: "",
      isHovering: false,
      isActiveTextFieldUsername: "",
      isActiveTextFieldPassword: "",
    };
  },
  methods: {
    async login() {
      const isFormGood = await this.v$.$validate();
      if (!isFormGood) return;
      this.isActive = true;
    },
    async clear() {
      this.username = "";
      this.password = "";
      await this.v$.$reset();
    },
    setTextFieldActive(eventTriggered) {
      if (eventTriggered == 1) {
        this.isActiveTextFieldPassword = "";
        this.isActiveTextFieldUsername = "primary primary--text";
      } else if (eventTriggered == 2) {
        this.isActiveTextFieldUsername = "";
        this.isActiveTextFieldPassword = "primary primary--text";
      }
    },
  },
  validations() {
    return {
      username: { required, email },
      password: { required },
    };
  },
};
</script>
