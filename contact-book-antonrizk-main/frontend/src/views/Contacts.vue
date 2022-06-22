<template>
    <!-- Navbar content -->
    <nav class="navbar navbar-expand-lg navbar navbar-light">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">Contact Book</a>
            <button
                class="navbar-toggler"
                type="button"
                data-bs-toggle="collapse"
                data-bs-target="#navbarSupportedContent"
                aria-controls="navbarSupportedContent"
                aria-expanded="false"
                aria-label="Toggle navigation"
            >
                <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarSupportedContent">
                <ul class="navbar-nav me-auto mb-2 mb-lg-0">
                    <li class="nav-item">
                        <a class="nav-link active" aria-current="page" href="#"
                            >Contacts</a
                        >
                    </li>
                    <li class="nav-item">
                        <router-link to="/create" class="nav-link active">
                            Add Contact</router-link
                        >
                    </li>
                </ul>
                <form class="d-flex" @submit.prevent>
                    <input
                        class="form-control me-2"
                        type="search"
                        placeholder="Search Contacts"
                        aria-label="Search"
                        v-model="search"
                    />
                    <button class="btn btn-outline-success">Search</button>
                </form>
            </div>
        </div>
    </nav>

    <div class="row">
        <div class="col-9 m-2">
            <h1 class="display-4">Contacts</h1>
        </div>
        <div class="d-flex justify-content-end m-2">
            <router-link to="/create" class="nav-link active">
                <button class="btn btn-outline-success" type="submit">
                    Add contact
                </button>
            </router-link>
        </div>

        <div class="row">
            <div class="col">
                <form class="form m-3" @submit.prevent>
                    <input
                        type="search"
                        class="form-control"
                        name="search"
                        placeholder="Search Contacts"
                        v-model="search"
                    />
                </form>
            </div>
        </div>
    </div>
    <div class="row">
        <div
            class="col col-12 col-md-6 col-lg-4 mb-3"
            v-for="contact in filteredContacts"
            :key="contact.id"
        >
            <router-link
                :to="'/contact/' + contact.id"
                class="text-decoration-none"
            >
                <div
                    class="card text-white bg-secondary mb-3"
                    style="max-width: 18rem"
                >
                    <div class="card-header">
                        <p>First Name: <br />{{ contact.first_name }}</p>
                    </div>
                    <div class="card-header">
                        <p>Last Name: <br />{{ contact.last_name }}</p>
                    </div>
                    <div class="card-body">
                        <p class="card-title">
                            Email: <br />{{ contact.email }}
                        </p>
                    </div>
                </div>
            </router-link>
        </div>
    </div>
</template>

<script>
export default {
    name: "Contacts",
    data: function () {
        return {
            contacts: [],
            search: "",
        };
    },

    created: async function () {
        //fetch call to the api
        //async & await.
        const response = await fetch(
            "http://contact-book-antonrizk.test/api/contacts"
        );
        const contacts = await response.json();

        this.contacts = contacts;
    },

    //search computed
    computed: {
        filteredContacts: function () {
            return this.contacts.filter(
                (contact) =>
                    contact.first_name
                        .toLowerCase()
                        .includes(this.search.toLowerCase()) ||
                    contact.last_name
                        .toLowerCase()
                        .includes(this.search.toLowerCase()) ||
                    contact.email
                        .toLowerCase()
                        .includes(this.search.toLowerCase())
            );
        },
    },
};
</script>
