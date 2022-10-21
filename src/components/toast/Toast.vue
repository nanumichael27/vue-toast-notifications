<template>
    <div class="toast bottom-left" :class="toastClasses" v-show="show">
        <div class="toast-icon">
            <component :is="toastIcon"></component>
        </div>
        <div class="toast-content">
            <div class="toast-title">{{toastTitle}}</div>
            <div class="toast-message">{{message}}</div>
        </div>
        <button @click="$emit('hide')" class="toast-button">&times;</button>
    </div>
</template>

<script>
import IconError from './IconError.vue'
import IconSuccess from './IconSuccess.vue'
import IconWarning from './IconWarning.vue'
export default {
    emits: ['hide'],
    data: () => ({
        timeout: null
    }),
    watch: {
       
        show () {
            if(this.timeout){
            clearTimeout(this.timeout);
            }
            this.timeout = setTimeout(() => {
            this.$emit('hide');
            }, 3000)
        }
    },
    props: {
        message:{
            type: String,
            required: true
        },
        title: {
            type: String,
            default: null
        },
        show:{
            type: Boolean,
            default: false
        },
        type:{
            type: String,
            default: 'success',
            validator: function(value) {
                return ['success', 'warning', 'error']
                .indexOf(value) !== -1;
            }
        },
        position: {
            type: String,
            default: 'bottom-right',
        }
    },
    components: {
        IconError,
        IconSuccess,
        IconWarning,
    },
    computed: {
        toastType() {
            return `toast-${this.getType}`;
        },
        toastIcon() {
            return `icon-${this.getType}`;
        },
        getType() {
            return ['success', 'warning', 'error']
                .indexOf(this.type) === -1 
                ? 'success'
                : this.type
        },
        toastTitle(){
            return this.title? this.title: 
            this.type.charAt(0).toUpperCase()
            + this.type.slice(1);
        },
        getPosition(){
            return ['bottom-left', 'bottom-right', 'top-left', 'top-right']
                .indexOf(this.position) === -1 
                ? 'bottom-right'
                : this.position
        },
        toastClasses() {
            return [this.toastType, this.getPosition]
        }
    }
}
</script>

<style scoped>
.toast{
    width: 300px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem;
    box-shadow: 1px 5px 10px -5px rgba(0, 0, 0, 0.4);
    position: relative;
}

.toast::before {
    content: '';
    width: 4px;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
}

.toast-icon {
    width: 16px;
    height: 16px;
    border-radius: 50%;
    padding: 7px;
}
/* success toasts */
.toast-success .toast-icon svg{
    fill: #ecfdf5;
}
.toast-success{
    background: #ecfdf5;
}
.toast-success::before, .toast-success .toast-icon{
    background: #34d399;
}
/* warning toasts */
.toast-warning .toast-icon svg{
    fill: #fffbeb;
}

.toast-warning{
    background: #fffbeb;
}

.toast-warning::before, .toast-warning .toast-icon{
    background: #f59e0b;
}
/* error toasts */

.toast-error .toast-icon svg{
    fill: #fef2f2;
}

.toast-error{
    background: #fef2f2;
}

.toast-error::before, .toast-error .toast-icon{
    background: #ef4444;
}

.toast-content{
    flex-grow: 1;
    margin: 0 1rem;
}

.toast-title {
    font-weight: 700;
    margin-bottom: 0.5rem;
}

.toast-message {
    font-size: 14px;
    color: #6b7280;
}

.toast-button{
    width: 1.5em;
    height: 1.5em;
    border: none;
    padding: 0;
    color: #9ca3af;
    opacity: 0.7;
    background: transparent;
    cursor: pointer;
    font-size: 1.5em;
}

.toast-button:hover{
    opacity: 1;
}

.bottom-left {
    position: fixed;
    left: 20px;
    bottom: 20px;
}

.top-left {
    position: fixed;
    left: 20px;
    top: 20px;
}

.bottom-right {
    position: fixed;
    right: 20px;
    bottom: 20px;
}

.top-right {
    position: fixed;
    right: 20px;
    bottom: 20px;
}
</style>