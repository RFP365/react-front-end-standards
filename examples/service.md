##Service Layer Example
`*.service.js` files serve as the interface layer for the api. 
They should utilize DTO Objects for shape and `*.routing.js` files for common variables.

````javascript
import {client} from '../baseClient';
import {supportRoutes} from './support.routing';

/**
 * Search for a list of companies whose name or clientId match the given search term
 * @param {any} _ the `react-query` cache key. ignored
 * @param {string} companySearchTerm the user-entered search term to filter companies by
 * @returns {Promise<import('@rfp360-web/common-services').CompanyDto[]>} the found companies
 */
export const searchCompanies = async (_, {companySearchTerm}) => {
    const {data, status} = await client.get(supportRoutes.searchCompanies, {
        params: {
            companySearchTerm: companySearchTerm || '',
        },
    });
    if (status !== 200 || data == null) {
        throw new Error('Unable to retrieve the Companies');
    }
    return data;
};

/**
 * A DTO for selecting the selecting and impersonating a company as a support engineer
 * @typedef {Object} SelectImpersonationCompanyDto
 * @property {string} selectedCompanyEId the encrypted id of the company to impersonate
 */

/**
 * A DTO representing the response of selecting a company to impersonate
 * @typedef {Object} CompanyImpersonatedResponseDto
 * @property {'SUCCESS' | 'FAILURE'} status the status of the operation of selecting a company to impersonate
 * @property {string} impersonatingCompanyEId the encrypted id of the company that is now being impersonated, null if failure
 * @property {string} homeComanyEId the authenticated users home company encrypted id
 */

/**
 * A company is being impersonated by a support engineer. Send the request with the company to impersonate
 * @param {SelectImpersonationCompanyDto} selectImpersonationCompany obj containing the selected company to impersonate
 * @returns {Promise<CompanyImpersonatedResponseDto>} the response from the API
 */
export const impersonateCompany = async (selectImpersonationCompany) => {
    const {data, status} = await client.patch(supportRoutes.impersonateCompany, selectImpersonationCompany);
    if (status !== 200 || data == null || data.status === 'FAILURE') {
        throw new Error('Unable to impersonate the selected company');
    }
    return data;
};
````
