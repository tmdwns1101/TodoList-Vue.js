<template>
    <transition name="modal">
        <div class="modal-mask">
            <div class="modal-wrapper">
                <div class="modal-container">
                    <div class="modal-header">
                        <slot name="header">
                            모달의 제목을 입력하세요.
                        </slot>
                    </div>
                    
                    <div class="modal-body">
                        <slot name="body">
                            모달의 컨텐츠를 입력하세요.
                        </slot>
                    </div>

                    <div class="modal-footer">
                        <button class="modal-btn" @click="confrim">확인</button>
                    </div>
                </div>
            </div>
        </div>
    
    </transition>
</template>

<script>
export default {
    
    methods: {
        confrim() {
            this.$emit('closeModal');
        }
    }
}
</script>

<style scoped>

    .modal-mask {
        position: fixed;
        z-index: 9998;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        background-color: rgba(0, 0, 0, .5);
        display: table;
        transition: opacity .3s ease;
    }

    .modal-wrapper {
        display: table-cell;
        vertical-align: middle;
    }

    .modal-container {
        position: relative;
        width: 200px;
        margin: 0px auto;
        padding: 20px 30px;
        background-color: #fff;
        box-shadow: 0 2px 8px rgba(0, 0, 0, .33);
        transition: all .3s ease;
        border-radius: 5px;
        
    }

    

    .modal-body {
        color: #339af0;
        font-weight: 400;
        font-size: 15px;
        font-family: 'Do Hyeon', sans-serif;
        
    }

    .modal-footer {
        margin-top: 5px;
        
    }

    .modal-btn {
        padding: 5px;
        border: none;
        
        color: #fa5252;
        font-size: 1rem;
        background: none;
        cursor: pointer;
        font-family: 'Do Hyeon', sans-serif;
    }


    .modal-enter {
        opacity: 0;
    }

    .modal-leave-active {
        opacity: 0;
    }

    .modal-enter .modal-container,
    .modal-leave-active .modal-container {
        -webkit-transform: scale(1.1);
        transform: scale(1.1);
    }
</style>