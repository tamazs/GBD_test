<template>
    <div v-if="showPopup" class="popup-overlay">
        <div class="popup">
            <h2>New Features Available</h2>
            <p>The name of your workspace will be visible to your customers. For us, it is "SAAS First". You will NOT be
                able to change this later.</p>
            <div class="feature-list">
                <p><strong>New UI/UX Designer</strong>
                    <span class="tooltip-container">
                        <i class="fas fa-circle-info" @mouseover="showTooltipDesigner = true"
                            @mouseleave="showTooltipDesigner = false"></i>
                        <span v-if="showTooltipDesigner" class="tooltip"><i class="fas fa-circle-info"></i>Lorem ipsum dolor
                            sit amet...</span>
                    </span>
                </p>
                <p><strong>New FE Developer</strong>
                    <span class="tooltip-container">
                        <i class="fas fa-circle-info" @mouseover="showTooltipDeveloper = true"
                            @mouseleave="showTooltipDeveloper = false"></i>
                        <span v-if="showTooltipDeveloper" class="tooltip"><i class="fas fa-circle-info"></i>Lorem ipsum
                            dolor sit amet...</span>
                    </span>
                </p>
            </div>
            <div class="feature-request">
                <label for="featureInput" @mouseover="showTooltip = true" @mouseleave="showTooltip = false"
                    @mousemove="updateTooltipPosition($event)">Request New Features
                    <span class="tooltip-container">
                        <i class="fas fa-circle-info" @mouseover="showTooltipLabel = true"
                            @mouseleave="showTooltipLabel = false"></i>
                        <span v-if="showTooltipLabel" class="tooltip"><i class="fas fa-circle-info"></i>Lorem ipsum dolor
                            sit amet...</span>
                    </span>
                </label>
                <input type="text" id="featureInput" placeholder="e.g. mobile app developer" v-model="featureRequest">
            </div>
            <div class="buttons">
                <button @click="closePopup">Cancel</button>
                <button @click="sendRequest" :disabled="isSendButtonDisabled"
                    :class="{ 'disabled': isSendButtonDisabled }">Send</button>
            </div>
        </div>
    </div>
</template>
  
<script setup>
import { ref, defineEmits, computed } from 'vue';

const emit = defineEmits(['close']);
const showPopup = ref(true);
const featureRequest = ref('');
const showTooltipDesigner = ref(false);
const showTooltipDeveloper = ref(false);
const showTooltipLabel = ref(false);

const closePopup = () => {
    emit('close');
};

const isSendButtonDisabled = computed(() => featureRequest.value.trim().length === 0);

const sendRequest = () => {
    closePopup();
};
</script>
  
<style scoped>
.popup-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
    background: rgba(0, 0, 0, 0.4);
}

.popup {
    background: white;
    padding: 2rem;
    border-radius: 10px;
    width: 80%;
    max-width: 500px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.popup h2 {
    text-align: center;
    font-size: 2.3rem;
    font-weight: normal;
}

.feature-list {
    margin: 2rem 0rem;
}

.feature-list p,
.feature-request label {
    font-weight: bold;
}

.feature-list p {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.feature-request input {
    width: 100%;
    padding: 0.5rem;
    margin-top: 0.5rem;
    margin-bottom: 1rem;
}

.buttons {
    display: flex;
    justify-content: space-between;
    gap: 1rem;
}

.buttons button {
    padding: 0.7rem 1rem;
    border: none;
    border-radius: 12px;
    cursor: pointer;
    width: 50%;
    font-size: 1rem;
}

.buttons button:first-child {
    background: #E9EFF2;
}

.buttons button:last-child {
    background: #3D22CF;
    color: white;
}

.buttons button.disabled {
    background: #ccc;
    cursor: not-allowed;
}

i {
    color: #9AA7AF;
}

label {
    display: flex;
    align-items: center;
    gap: 0.5rem;
}

.tooltip {
    position: absolute;
    padding: 1rem;
    background: rgb(231, 231, 231);
    color: black;
    border-radius: 4px;
    z-index: 100;
    display: flex;
    align-items: center;
    font-weight: normal;
    font-size: 1rem;
}

.tooltip i {
    margin-right: 0.5rem;
    font-size: 1.5rem;
}
</style>
  