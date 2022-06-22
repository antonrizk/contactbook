<template>
    <div class="row my-5 d-flex align-items-center">
        <div class="col-9">
            <h1 class="display-4">Edit Contact</h1>
        </div>
    </div>
    <div class="row">
        <div class="col">
            <form
                @submit.prevent="updateContact"
                class="form mb-3 d-flex flex-column bg-light p-5"
            >
                <label for="First name" class="form-label">First name</label>
                <input
                    type="text"
                    class="form-control mb-3"
                    name="first name"
                    v-model="first_name"
                />

                <label for="Last name" class="form-label">Last name</label>
                <input
                    type="text"
                    class="form-control mb-3"
                    name="last name"
                    v-model="last_name"
                />

                <label for="Email" class="form-label">Email</label>
                <input
                    type="text"
                    class="form-control mb-3"
                    name="email"
                    v-model="email"
                />
                <div class="align-self-end">
                    <router-link
                        :to="`/contact/${id}`"
                        class="btn btn-secondary me-3"
                        >Cancel</router-link
                    >
                    <button class="btn btn-primary">Update Contact</button>
                </div>
            </form>

            <div class="d-flex justify-content-center">
                <button class="btn btn-outline-danger" @click="deleteContact">
                    Delete Contact
                </button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Edit",
    props: ["id"],
    data: function () {
        return {
            first_name: "",
            last_name: "",
            email: "",
        };
    },
    created: async function () {
        const response = await fetch(
            "http://contact-book-antonrizk.test/api/contacts/" + this.id
        );
        const contact = await response.json();

        this.first_name = contact.first_name;
        this.last_name = contact.last_name;
        this.email = contact.email;
    },

    methods: {
        updateContact: async function () {
            const contact = {
                first_name: this.first_name,
                last_name: this.last_name,
                email: this.email,
            };
            const response = await fetch(
                "http://contact-book-antonrizk.test/api/contacts/" + this.id,
                {
                    method: "PUT",
                    body: JSON.stringify(contact),
                    headers: {
                        "Content-Type": "application/json",
                    },
                }
            );
            const json = await response.json();

            this.$router.push("/contact/" + json.id);
        },
        deleteContact: async function () {
            const response = await fetch(
                "http://contact-book-antonrizk.test/api/contacts/" + this.id,
                {
                    method: "DELETE",
                    headers: {
                        "Content-Type": "application/json",
                    },
                }
            );
            this.$router.push("/");
        },
    },
};
</script>
