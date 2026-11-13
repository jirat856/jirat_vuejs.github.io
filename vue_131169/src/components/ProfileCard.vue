<script setup lang="ts">
interface Profile {
    name: string
    role: string
    bio: string
    image: string
    skills: string[]
}

defineProps<{
    profile: Profile
}>()
</script>

<template>
    <div class="profile-card">
        <div class="card-image-wrapper">
            <img :src="profile.image" :alt="profile.name" class="profile-image" />
        </div>
        <div class="card-content">
            <h3 class="profile-name">{{ profile.name }}</h3>
            <p class="profile-role">{{ profile.role }}</p>
            <p class="profile-bio">{{ profile.bio }}</p>

            <div class="profile-skills">
                <span v-for="(skill, index) in profile.skills" :key="index" class="skill-tag">
                    {{ skill }}
                </span>
            </div>
        </div>
    </div>
</template>

<style scoped>
.profile-card {
    background: #ffffff;
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
    max-width: 400px;
    margin: 0 auto;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.profile-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 25px rgba(0, 0, 0, 0.12);
}

.card-image-wrapper {
    width: 100%;
    height: 220px;
    overflow: hidden;
    background-color: #f0f2f5;
}

.profile-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
}

.card-content {
    padding: 1.5rem;
}

.profile-name {
    font-size: 1.3rem;
    font-weight: bold;
    color: #333;
    margin-bottom: 0.25rem;
}

.profile-role {
    font-size: 0.9rem;
    color: #3498db;
    font-weight: 600;
    margin-bottom: 0.75rem;
}

.profile-bio {
    font-size: 0.95rem;
    color: #666;
    line-height: 1.4;
    margin-bottom: 1rem;
}

.profile-skills {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
}

.skill-tag {
    background-color: #eef2f7;
    color: #4a5568;
    font-size: 0.75rem;
    padding: 0.2rem 0.6rem;
    border-radius: 20px;
    font-weight: 500;
}
</style>