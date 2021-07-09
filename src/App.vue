<template>
    <div>
        <h1>{{title}}</h1>
        <input type="text" ref="name">
        <button @click="handleClick">Click Me</button>
        <p></p>
        <div v-if="showModal">
            <Modal
                header="Modal Header"
                @close="handleModal"
            >
                <p>Modal Content</p>
                <template v-slot:links>
                    <a href="#">Sign Up</a>
                    <a href="#">Sign In</a>
                </template>
            </Modal>
        </div>
        <div v-if="login">
            <Modal
                header="Login With Email and Password"
                @close="handleModal('login')"
            >
                <template v-slot:login>
                    <input type='text' name='email' placeholder="Email">
                    <input type='password' name='password' placeholder="Password">
                    <button>Login</button>
                </template>
            </Modal>
        </div>

        <div v-if="signup">
            <Modal
                header="Sign Up new user"
                @close="handleModal('signup')"
            >
                <template v-slot:signup>
                    <input type='text' name='email' placeholder="Email">
                    <input type='password' name='password' placeholder="Password">
                    <input type='password' name='confirmpassword' placeholder="Confirm Password">
                    <button>Sign Up</button>
                </template>
            </Modal>
        </div>
        
        <button @click="handleModal()">Open Modal</button>
        <button @click="handleModal('login')">Login In</button>
        <button @click="handleModal('signup')">Sign Up</button>
    </div>
</template>

<script>
import Modal from './components/Modal';

export default {
    name: 'App',
    components : { Modal },
    data() {
        return {
            title : 'My First Vue App',
            header : 'Login With Email and Password',
            content : 'Modal Content',
            showModal : false,
            login : false,
            signup : false
        }
    },
    methods : {
        handleClick()
        {
            this.$refs.name.classList.add('active');
        },
        handleModal(modalType)
        {
            if(modalType === 'login')
            {
                this.login = !this.login;
                this.signup = false;
                this.showModal = false;
            }
            else if(modalType === 'signup')
            {
                this.login = false;
                this.signup = !this.signup;
                this.showModal = false;
            }
            else
            {
                this.showModal = !this.showModal;
                this.login = false;
                this.signup = false;
            }
        }
    }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
