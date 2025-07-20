<script setup>
import { ref, onMounted } from 'vue';
import UserLayout from '@/layouts/UserLayout.vue';

// import { Winter } from '@/components/images';
// const images = [Winter]

const profileImageUrl = ref('src/components/images/winter.jpg')
const email = ref('')
const name = ref('')

const handleFileUpload = (event) => {
    const file = event.target.files[0]

    if (file) {
        const reader = new FileReader()
        reader.onload = (e) => {
            profileImageUrl.value = e.target.result
        }
        reader.readAsDataURL(file)
    }
}

const updateProfile = () => {
    const profileData = {
        imageUrl: profileImageUrl.value,
        name: name.value,
        email: email.value
    }
    localStorage.setItem('profile-Data', JSON.stringify(profileData))
    alert('Update Profile Successfully')
}

onMounted(() => {
    let profileData = localStorage.getItem('profile-Data')
    if (profileData) {
        profileData = JSON.parse(profileData)
        profileImageUrl.value = profileData.imageUrl
        name.value = profileData.name
        email.value = profileData.email
    }
})

</script>

<template>
    <UserLayout>
        <div class="max-w-2xl mx-auto border border-base-200 shadow-xl p-8 my-4">
            <div class="text-2xl font-bold">Your Profile ✨</div>

            <div class="flex flex-col items-center">
                <div class="flex flex-col items-center">
                    <div class="avatar">
                        <div class="w-24 rounded-full">
                            <img :src="profileImageUrl">
                        </div>
                    </div>
                    <input type="file" @change="handleFileUpload">
                </div>
                <div class="form-control w-full">
                    <label class="label">
                        <b><span class="label-text">Email</span></b>
                    </label>
                    <input v-model="email" type="text" placeholder="Type here" class="input input-bordered w-full rounded-3xl">
                </div>
                <div class="form-control w-full">
                    <label class="label">
                        <b><span class="label-text">Name</span></b>
                    </label>
                    <input v-model="name" type="text" placeholder="Type here" class="input input-bordered w-full rounded-3xl">
                </div>
                <button @click="updateProfile" class="btn btn-neutral w-full mt-4 rounded-3xl">UPDATE PROFILE</button>
            </div>
        </div>
    </UserLayout>
</template>