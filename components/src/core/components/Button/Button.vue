<!--
/*
 * This file is part of OrangeHRM Inc
 *
 * Copyright (C) 2020 onwards OrangeHRM Inc
 *
 * This program is free software; you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation; either version 3 of the License, or
 * (at your option) any later version.
 *
 * This program is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with this program.  If not, see  http://www.gnu.org/licenses
 */
-->

<template>
  <button type="button" :class="classes" :style="style">
    <slot name="icon">
      <oxd-icon v-if="iconName" :name="iconName" class="oxd-button-icon" />
    </slot>
    {{ label }}
    <slot name="iconRight">
      <oxd-icon
        v-if="iconRightName"
        :name="iconRightName"
        class="oxd-button-icon"
      />
    </slot>
  </button>
</template>

<script lang="ts">
import {defineComponent} from 'vue';
import {
  ButtonSize,
  ButtonType,
  SIZES,
  SIZE_MEDIUM,
  TYPES,
  TYPE_MAIN,
} from './types';
import Icon from '@ohrm/oxd/core/components/Icon/Icon.vue';

export default defineComponent({
  name: 'oxd-button',

  components: {
    'oxd-icon': Icon,
  },

  props: {
    label: {
      type: String,
      required: true,
    },
    displayType: {
      type: String,
      default: TYPE_MAIN,
      validator: function(value: ButtonType) {
        return TYPES.indexOf(value) !== -1;
      },
    },
    size: {
      type: String,
      default: SIZE_MEDIUM,
      validator: function(value: ButtonSize) {
        return SIZES.indexOf(value) !== -1;
      },
    },
    style: {
      type: Object,
    },
    iconName: {
      type: String,
    },
    iconRightName: {
      type: String,
    },
  },

  computed: {
    classes(): object {
      return {
        'oxd-button': true,
        [`oxd-button--${this.size}`]: true,
        [`oxd-button--${this.displayType}`]: true,
      };
    },
  },
});
</script>

<style src="./button.scss" lang="scss" scoped></style>
