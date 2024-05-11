<template>
    <div class="main-wrapper">
        <div class="account-content">
            <div class="login-wrapper">
                <div class="login-content">

                  <div class="login-userset">
                    <div class="login-logo logo-normal">
                    <img src="/src/assets/img/logo.png" alt="img">
                    </div>
                    <a href="#" class="login-logo logo-white">
                      <img src="/src/assets/img/logo.png"  alt="">
                    </a>
                    <div class="login-userheading">
                      <h3>Sign In</h3>
                      <h4>Please login to your account</h4>
                    </div>
                    <div class="form-login">
                      <label>Username</label>
                      <div class="form-addons">
                        <input type="text" placeholder="Enter your username" v-model="username"/>
                        <img src="/src/assets/img/icons/mail.svg" alt="img" />
                      </div>
                    </div>
                    <div class="form-login">
                      <label>Password</label>
                      <div class="pass-group">
                        <input class="pass-input" placeholder="Enter your password" v-model="password"/>
                        <span class="fas toggle-password fa-eye-slash"></span>
                      </div>
                    </div>
                    <div class="form-login">
                      <a class="btn btn-login">Sign In</a>
                    </div>
                  </div>
                </div>
                <div class="login-img">
                    <img src="/src/assets/img/login.jpg" alt="img" />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    data () {
        return{
            username: '',
            password: ''
        }
    },
    methods: {
        async login() {
            try{
                const response = await fetch('http://127.0.0.1:8000/login/user', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify({
                        username: this.username,
                        password: this.password
                    })
                });

                if (response.ok) {
                    const data = await response.json();
                    const accessToken = data.access_token;
                    localStorage.setItem('accessToken', accessToken);
                    this.$router.push('/home');
                } else {
                    console.error('Login failed');
                }
            } catch (error) {
                console.error('Error:', error);
            }
        } 
    }

}
</script>
