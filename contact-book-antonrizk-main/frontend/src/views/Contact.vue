<template>
    <div class="row my-5 d-flex align-items-center">
        <div class="col-9">
            <h1 class="display-4">Contact</h1>
        </div>
        <div class="d-flex justify-content-end m-2">
            <router-link
                :to="'/contact/' + id + '/edit'"
                class="nav-link active"
            >
                <button class="btn btn-outline-success">Edit</button>
            </router-link>
        </div>
    </div>
    <!-- <div class="row">
        <div class="col ms-4">
            <p class="display-6 text-success">Info</p>
        </div>
    </div> -->
    <div class="row d-flex justify-content-center">
        <div class="card text-white bg-secondary mb-3" style="max-width: 30rem">
            <div class="card-header">
                <p>First Name: <br />{{ first_name }}</p>
            </div>
            <div class="card-header">
                <p>Last Name: <br />{{ last_name }}</p>
            </div>
            <div class="card-body">
                <p class="card-title">Email: <br />{{ email }}</p>
            </div>
        </div>
    </div>
    <div class="row">
        <router-link to="/" class="text-decoration-none">
            <button class="btn btn-outline-success">Back</button></router-link
        >
    </div>
</template>

<script>
export default {
    name: "Contact",
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
};
</script>
