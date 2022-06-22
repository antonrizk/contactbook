<template>
    <div class="row my-5 d-flex align-items-center">
        <div class="col-9">
            <h1 class="display-4">Add Contact</h1>
        </div>
    </div>
    <div class="row">
        <div class="col">
            <form
                @submit.prevent="addContact"
                class="form mb-3 d-flex flex-column bg-light p-5"
            >
                <label for="First name" class="form-label">First name</label>
                <input
                    type="text"
                    class="form-control mb-3"
                    name="title"
                    v-model="first_name"
                />

                <label for="Last name" class="form-label">Last name</label>
                <input
                    class="form-control mb-3"
                    name="text"
                    v-model="last_name"
                />

                <label for="Email" class="form-label">Email</label>
                <input class="form-control mb-3" name="text" v-model="email" />

                <div class="align-self-end">
                    <router-link to="/" class="btn btn-secondary me-3"
                        >Cancel</router-link
                    >
                    <button class="btn btn-primary">Add Contact</button>
                </div>
            </form>
        </div>
    </div>
</template>

<script>
export default {
    name: "Create",
    data: function () {
        return {
            first_name: "",
            last_name: "",
            email: "",
        };
    },
    methods: {
        addContact: async function () {
            const contact = {
                first_name: this.first_name,
                last_name: this.last_name,
                email: this.email,
            };

            const response = await fetch(
                "http://contact-book-antonrizk.test/api/contacts",
                {
                    method: "POST",
                    body: JSON.stringify(contact),
                    headers: {
                        "Content-Type": "application/json",
                    },
                }
            );
            const json = await response.json();

            this.$router.push("/contact/" + json.id);
        },
    },
};
</script>
