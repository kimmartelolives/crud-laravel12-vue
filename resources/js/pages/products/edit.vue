<script setup lang="ts">
import Button from '@/components/ui/button/Button.vue';
import Input from '@/components/ui/input/Input.vue';
import Label from '@/components/ui/label/Label.vue';
import AppLayout from '@/layouts/AppLayout.vue';
import { type BreadcrumbItem } from '@/types';
import { Head } from '@inertiajs/vue3';
import { useForm } from '@inertiajs/vue3'

interface Product {
    id: number;
    name: string;
    price: number;
    description: string;
}

const props = defineProps<{ product: Product }>();

const form = useForm({
    name: props.product.name,
    price: props.product.price,
    description: props.product.description,
});

const handleSubmit = () => {
    form.put(route('products.update', {product:props.product.id}));
};
</script>

<template>

    <Head title="Edit a Product" />

    <AppLayout :breadcrumbs="[
        {
            title: 'Edit a Product',
            href: `/products/${props.product.id}/edit`,
        },]">

        <div class="p-4">
            <form @submit.prevent="handleSubmit" class="w-8/12 space-y-4">
                <div class="space-y-2">
                    <Label for="Product Name">Name</Label>
                    <Input v-model="form.name" type="text" placeholder="Name"></Input>
                    <div class="text-sm text-red-600" v-if="form.errors.name">{{ form.errors.name }}</div>
                </div>

                <div class="space-y-2">
                    <Label for="Product Price">Price</Label>
                    <Input v-model="form.price" type="number" placeholder="Price"></Input>
                    <div class="text-sm text-red-600" v-if="form.errors.price">{{ form.errors.price }}</div>
                </div>

                <div class="space-y-2">
                    <Label for="Product Description">Description</Label>
                    <Input v-model="form.description" type="text" placeholder="Description"></Input>
                    <div class="text-sm text-red-600" v-if="form.errors.description">{{ form.errors.description }}</div>
                </div>

                <Button type="submit" :disabled="form.processing">Edit a Product</Button>
            </form>
        </div>
    </AppLayout>
</template>
