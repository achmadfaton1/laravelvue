<template>
    <div class="container my-5">
        <div class="row justify-content-center">
            <div class="col-8">
                <!-- <a href="/create">tes</a> -->
                <router-link 
                    :to="{ path: '/create'}" class="btn btn-primary btn-sm"
                >Add</router-link>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>